<template>
  <div id="register" class="d-flex flex-column align-items-center text-center" style="padding: 0px 37px;margin-top: 60px">
    <h3 class="text-center text-primary">線上保證書<br></h3>
    <Form @submit="store" :validation-schema="schema" v-slot="{ errors, values, validate }" style="max-width:500px">
      <div style="display:none">{{ errors }}{{ values }}</div>
      <div style="display:none">{{ validate }}</div>
      <div class="form-group text-left">
        <label class="form_label">機身序號<span class="text-danger" style="padding-left: 3px;">*</span></label>
        <Field v-model="form.code" class="form-control" type="text" id="保固序號" name="保固序號" placeholder="請刮開外包裝保固貼紙序號"
                   :class="{ 'is-invalid': errors['保固序號'] }" rules="required"></Field>
        <error-message name="保固序號" class="invalid-feedback"></error-message>
      </div>
      <div class="form-row">
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">姓名<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <Field v-model="form.name" class="form-control" type="text" id="姓名" name="姓名"
                   :class="{ 'is-invalid': errors['姓名'] }" rules="required"></Field>
            <error-message name="姓名" class="invalid-feedback"></error-message>
          </div>
        </div>
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">手機<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <Field id="phone" name="手機" v-model="form.tel" class="form-control" type="text"
                   :rules="isPhone" :class="{ 'is-invalid': errors['手機'] }"></Field>
            <error-message name="手機" class="invalid-feedback"></error-message>
          </div>
        </div>
      </div>
      <div class="form-row">
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">地址<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <div class="d-flex">
              <select id="縣市" name="縣市" class="form-control w-50" v-model="form.county"
              :class="{ 'is-invalid': errors['縣市'] }" rules="required">
                <option value="" disabled>縣市</option>
                <option v-for="(item, key) in aryCity" v-bind:key="key" :value="item">{{ item }}</option>
              </select>
              <select id="鄉鎮市區" class="district form-control w-25" v-model="form.district" @change="getZip">
                <option value="" disabled>鄉鎮市區</option>
                <option v-for="(item, key) in filterData" v-bind:key="key" :value="item.city">{{ item.city }}</option>
              </select>
              <Field class="input w-25" id="郵遞區號" name="郵遞區號" v-model="form.zipcode" type="text" placeholder="郵遞區號" 
              :class="{ 'is-invalid': errors['郵遞區號'] }" rules="required" as="input"></Field>
              <error-message name="郵遞區號" class="invalid-feedback"></error-message>
            </div>
            <p>{{ form.county }}、{{ form.district }}、{{ form.zipcode }}、{{ form.shop }}</p>
          </div>
          <div class="form-group text-left">
            <Field v-model="form.address" class="form-control" type="text" id="地址" name="地址"
                   :class="{ 'is-invalid': errors['地址'] }" rules="required"></Field>
            <error-message name="地址" class="invalid-feedback"></error-message>
          </div>
        </div>
      </div>
      <div class="form-group text-left">
        <label class="form_label">E-mail</label>
        <!-- email 必填驗證 -->
        <input id="email" name="email" class="form-control" type="email" placeholder="請輸入 Email">
        <!-- <Field id="email" name="email" class="form-control" type="email" placeholder="請輸入 Email"
               :class="{ 'is-invalid': errors['email'] }" rules="email|required"></Field>
        <error-message name="email" class="invalid-feedback"></error-message> -->
      </div>
      <div class="form-group text-left">
        <label class="form_label">發票號碼</label>
        <input v-model="form.invoice" class="form-control" type="text">
      </div>
      <div class="form-group text-left">
        <label class="form_label">購買通路<span class="text-danger" style="padding-left: 3px;">*</span></label>
        <div class="d-flex align-items-center flex-wrap">
          <template v-for="item in items" v-bind:key="item.key">
            <div v-if="item.key=='seller'" v-bind:key="item.key" class="d-flex align-items-center" style="width: fit-content; margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="margin-right: 8px;">
                <Field type="radio" name="shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input"></Field>
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.seller" class="form-control" type="text" placeholder="業務姓名或 N" style="width: 135px;margin-right: 8px;">
            </div>
            <div v-else-if="item.key=='others'" v-bind:key="item.key" class="d-flex align-items-center" style="width: fit-content;margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="min-width: 65px;margin-right: 8px;">
                <Field type="radio" name="shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input"></Field>
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.others" class="form-control" type="text" placeholder="請填寫" style="width: 175px;">
            </div>
            <div v-else v-bind:key="item.key" class="custom-control custom-control-inline custom-radio">
              <Field type="radio" name="shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input"></Field>
              <label :for="item.key" class="custom-control-label">{{ item.value }}</label>
            </div>
          </template>
        </div>
        <error-message name="shop" class="text-danger error-text"></error-message>
      </div>
      <div class="d-flex"></div>
      <button class="btn btn-primary btn-block" type="submit" style="margin-top: 15px;">送出</button>
    </Form>
    <ul class="remark">
      <li class="text-justify" style="margin-bottom: 5px;padding-top: 20px;">※注意事項：本產品全球不提供維修,台灣代理商提供公司正貨保固兩年內更換服務。</li>
      <li class="text-justify text-danger" style="margin-bottom: 30px">※本保固服務僅適用於正常使用情況或非人為因素導致之故障。</li>
    </ul>
  </div>
</template>

<script>
// /* global $ */  載入套件 jQuery
import twzipcode from 'twzipcode-data'

export default {
  data () {
    const schema = {
      保固序號: 'required|min:10',
      手機: 'required|min:10',
      shop: (value) => {
        if (value) {
          return true;
        }
        return '你需要選擇 "購買通路"';
      },
      郵遞區號: (value) => {
        if (value) {
          return true;
        }
        return '請確實填寫 "縣市、區域、郵遞區號"';
      }
    }
    return {
      schema,
      form: {
        code: '',
        name: '',
        tel: '',
        county: '',
        district: '',
        zipcode: '',
        address: '',
        email: null,
        invoice: null,
        shop: '',
        seller: '',
        others: ''
      },
      items: [
        { key: 'department', value: '百貨專櫃' },
        { key: 'drug', value: '藥局診所' },
        { key: 'online', value: '網路購買' },
        { key: 'gift', value: '親友贈送' },
        { key: 'seller', value: '專員訂購' },
        { key: 'others', value: '其他' }
      ],
      errors: {},
      aryCity: [], // (189 行)(38 行)假設縣市名稱 ("縣市" 名稱 v-for 寫回介面)
      cities: '', // 由套件撈取的資料 (縣市名稱)  [{id: "臺北市", name: "臺北市"}, ....]
      zipCode: '' // 由套件撈取的資料 (郵地區號)  [{id: 100, county: "臺北市", city: "中正區"},...]
    }
  },
  computed: {
    filterData () {
      const vm = this
      let getCity = [] // 篩選過後的縣市 [{id: 100, county: "臺北市", city: "中正區"},...]
      if (vm.form.county !== '') {
        getCity = vm.zipCode.filter(item => item.county === vm.form.county)
      }
      return getCity // 篩選出 [{id: 100, county: "臺北市", city: "中正區"},...]
    }
  },
  methods: {
    getZip (e) { // "縣市區域名" 欄位綁 change 監聽
      console.log(e.target.value) // 取出 "縣市區域名" : "仁愛區"
      const vm = this
      let zipNum = []
      if (e.target.value !== '') {
        zipNum = vm.zipCode.filter(item => item.county === vm.form.county && item.city === vm.form.district)
      }
      vm.form.zipcode = zipNum[0].id
    },
    getZipCode () {
      const vm = this
      vm.zipCode = twzipcode().zipcodes
      vm.cities = twzipcode().counties
      // console.log(vm.zipCode) // 取得各縣市的郵遞區號
      // console.log(vm.cities) // 取得各縣市名稱 (不重複)
      for (let i = 0; i < 22; i++) {
        vm.aryCity.push(vm.cities[i].id)
      }
    },
    store () {
      const vm = this
      //   const endpoint = `${process.env.MIX_API_URL}/warranty`

      //   this.flash(null)
      //   this.errors = {}


      //   vm.$http.post(endpoint, this.form)
      //     .then(response => {
      //       this.reset()
      //       this.flash(response.data.message)
      //     })
      //     .catch(e => {
      //       this.errors = e.response.data.errors
      //     })
      console.log(vm.form)
    },
    isPhone (value) {
      const phoneNumber = /^(09)[0-9]{8}$/
      return phoneNumber.test(value) ? true : '需要正確的電話號碼'
    },
    reset () {
      const vm = this
      vm.form.code = ''
      vm.form.name = ''
      vm.form.tel = ''
      vm.form.county = ''
      vm.form.district = ''
      vm.form.zipcode = ''
      vm.form.address = ''
      vm.form.email = null
      vm.form.invoice = null
      vm.form.shop = ''
      vm.form.seller = null
      vm.form.others = null
      $('#twzipcode').twzipcode('reset')
    }
  },
  created () {
    const vm = this
  //   // 後台 api
  //   const api = 'http://wwwtest.mira-teeth.com.tw/admin/api/shop'
  //   vm.$http.get(api).then(response => {
  //     vm.items = response.data
  //     console.log(vm.items)
  //   })
  vm.getZipCode()
  }
}
</script>
