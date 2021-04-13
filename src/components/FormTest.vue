<template>
<div id="formTable" class="col-md-6 text-center" style="padding: 0px 37px;">
    <h3 class="text-center text-primary">FormData<br></h3>
    <Form @submit="store" v-slot="{ errors, values, validate }" style="max-width:500px">
      <div>{{ errors }}{{ values }}</div>
      <div style="display:none">{{ validate }}</div>
      <div class="form-group text-left">
        <label class="form_label">機身序號<span class="text-danger" style="padding-left: 3px;">*</span></label>
        <input v-model="form.code" class="form-control" type="text" placeholder="請刮開外包裝保固貼紙序號">
        <span v-if="errors.code">
          <small class="text-danger">{{ errors.code[0] }}</small>
        </span>
      </div>
      <div class="form-row">
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">姓名<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <Field id="name" name="姓名" :rules="isRequired" v-model="form.name"
            class="form-control" type="text" :class="{ 'is-invalid': errors['姓名'] }"></Field>
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
            <!-- <div id="twzipcode" class="d-flex"> -->
            <div class="d-flex">
              <select id="縣市" class="form-control w-50" v-model="form.county">
                <option value="" disabled>縣市</option>
                <option v-for="(item, key) in aryCity" v-bind:key="key" :value="item">{{ item }}</option>
              </select>
              <select id="鄉鎮市區" class="form-control w-50" v-model="form.district">
                <option value="" disabled>鄉鎮市區</option>
                <option v-for="(item, key) in filterData" v-bind:key="key" :value="item">{{ item.city }}</option>
              </select>
              <input type="text" :value="form.zipcode" class="w-25">  <!--v-mdoel="form.zipcode"-->
              <!-- <div data-role="county" data-name="county"
                data-style="form-control" class="w-50">
              </div>
              <div data-role="district" data-name="district[]"
                data-style="form-control" class="w-25">
              </div>
              <div data-role="zipcode" data-name="zipcode"
                data-style="form-control" class="w-25">
              </div> -->
            </div>
            <!-- <span v-if="errors.zipcode">
              <small class="text-danger">{{ errors.zipcode[0] }}</small>
            </span> -->
          </div>
          <div class="form-group text-left">
            <Field v-model="form.address" id="地址" name="地址" class="form-control" type="text"
            :class="{ 'is-invalid': errors['地址'] }" rules="required"></Field>
            <error-message name="地址" class="invalid-feedback"></error-message>
          </div>
        </div>
      </div>
      <div class="form-group text-left">
        <label class="form_label">E-mail</label>
        <Field id="email" name="email" class="form-control" type="email" placeholder="請輸入 Email"
               :class="{ 'is-invalid': errors['email'] }" rules="email|required"></Field>
        <error-message name="email" class="invalid-feedback"></error-message>
      </div>
      <div class="form-group text-left">
        <label class="form_label">發票號碼</label>
        <input v-model="form.invoice" class="form-control" type="text">
      </div>
      <div class="form-group text-left">
        <label class="form_label">購買通路<span class="text-danger" style="padding-left: 3px;">*</span></label>
        <div class="d-flex align-items-center flex-wrap">
          <template v-for="item in items" :key="item.key">
            <div v-if="item.key=='seller'" :key="item.key" class="d-flex align-items-center" style="width: fit-content; margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="margin-right: 8px;">
                <input type="radio" name="form.shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input" checked>
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.seller" class="form-control" type="text" placeholder="業務姓名或 N" style="width: 135px;margin-right: 8px;">
            </div>
            <div v-else-if="item.key=='others'" :key="item.key" class="d-flex align-items-center" style="width: fit-content;margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="min-width: 65px;margin-right: 8px;">
                <input type="radio" name="form.shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input">
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.others" class="form-control" type="text" placeholder="請填寫" style="width: 175px;">
            </div>
            <div v-else :key="item.key" class="custom-control custom-control-inline custom-radio">
              <input type="radio" name="form.shop" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input">
              <label :for="item.key" class="custom-control-label">{{ item.value }}</label>
            </div>
          </template>
          <span v-if="errors.shop">
            <small class="text-danger">{{ errors.shop[0] }}</small>
          </span>
        </div>
      </div>
      <div class="d-flex"></div>
      <button class="btn btn-primary btn-block" type="submit" style="margin-top: 15px;margin-bottom: 30px;">送出</button>
    </Form>
  </div>
</template>
<script>
// /* global $ */
import twzipcode from 'twzipcode-data'

export default {
  data () {
    return {
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
        seller: null,
        others: null
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
      aryCity: [], // (150 行)假設縣市名稱
      cities: '', // 由套件撈取的資料
      zipCode: '' // 由套件撈取的資料
    }
  },
  computed: {
    filterData () {
      const vm = this
      let getCity = [] // 篩選過後的縣市 [{id: 100, county: "臺北市", city: "中正區"},...]
      let zip = []
      if (vm.form.county !== '') {
        getCity = vm.zipCode.filter(item => item.county === vm.form.county)
        if (vm.form.district !== '') {
          zip = getCity.filter(item => item.city === vm.form.district)
          zip.forEach(item => {
            vm.form.zipcode = item.id
          })
        }
      }
      return getCity
    }
  },
  methods: {
    getZipCode () {
      const vm = this
      vm.zipCode = twzipcode().zipcodes
      vm.cities = twzipcode().counties
      console.log(vm.zipCode) // 取得各縣市的郵遞區號
      // console.log(vm.cities) // 取得各縣市名稱 (不重複)
      for (let i = 0; i < 22; i++) {
        vm.aryCity.push(vm.cities[i].id)
      }
    },
    store () {
      console.log(this.form)
    },
    reset () {
      this.form.code = ''
      this.form.name = ''
      this.form.tel = ''
      this.form.county = ''
      this.form.district = ''
      this.form.zipcode = ''
      this.form.address = ''
      this.form.email = null
      this.form.invoice = null
      this.form.shop = ''
      this.form.seller = null
      this.form.others = null
      // $('#twzipcode').twzipcode('reset')
    }
  },
  // mounted () {
  //   const vm = this
  //   const api = 'http://wwwtest.mira-teeth.com.tw/admin/api/shop'
  //   vm.$http.get(api).then(response => {
  //     vm.items = response.data
  //     console.log(vm.items)
  //   })
  //   // $('#twzipcode').twzipcode()
  // },
  created () {
    const vm = this
    vm.getZipCode()
    console.log(vm.aryCounty)
  }
}
</script>
