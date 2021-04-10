<template>
<div id="register" class="col-md-6 text-center" style="padding: 0px 37px;">
    <h3 class="text-center text-primary">FormData<br></h3>
    <alert></alert>
    <form @submit.prevent="store" class="mb-10">
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
            <input v-model="form.name" class="form-control" type="text">
            <span v-if="errors.name">
              <small class="text-danger">{{ errors.name[0] }}</small>
            </span>
          </div>
        </div>
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">手機<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <input v-model="form.tel" class="form-control" type="text">
            <span v-if="errors.tel">
              <small class="text-danger">{{ errors.tel[0] }}</small>
            </span>
          </div>
        </div>
      </div>
      <div class="form-row">
        <div class="col">
          <div class="form-group text-left">
            <label class="form_label">地址<span class="text-danger" style="padding-left: 3px;">*</span></label>
            <div id="twzipcode" class="d-flex">
              <div data-role="county" data-name="county"
                data-style="form-control" class="w-50">
              </div>
              <div data-role="district" data-name="district[]"
                data-style="form-control" class="w-25">
              </div>
              <div data-role="zipcode" data-name="zipcode"
                data-style="form-control" class="w-25">
              </div>
            </div>
            <span v-if="errors.zipcode">
              <small class="text-danger">{{ errors.zipcode[0] }}</small>
            </span>
          </div>
          <div class="form-group text-left">
            <input v-model="form.address" class="form-control" type="text">
            <span v-if="errors.address">
              <small class="text-danger">{{ errors.address[0] }}</small>
            </span>
          </div>
        </div>
      </div>
      <div class="form-group text-left">
        <label class="form_label">E-mail</label>
        <input v-model="form.email" class="form-control" type="email">
      </div>
      <div class="form-group text-left">
        <label class="form_label">發票號碼</label>
        <input v-model="form.invoice" class="form-control" type="text">
      </div>
      <div class="form-group text-left">
        <label class="form_label">購買通路<span class="text-danger" style="padding-left: 3px;">*</span></label>
        <div class="d-flex align-items-center flex-wrap">
          <template v-for="item in items">
            <div v-if="item.key=='seller'" :key="item.key" class="d-flex align-items-center" style="width: fit-content; margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="margin-right: 8px;">
                <input type="radio" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input">
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.seller" class="form-control" type="text" placeholder="業務姓名或 N" style="width: 135px;margin-right: 8px;">
            </div>
            <div v-else-if="item.key=='others'" :key="item.key" class="d-flex align-items-center" style="width: fit-content;margin: 5px 0px;">
              <div class="custom-control custom-control-inline custom-radio" style="min-width: 65px;margin-right: 8px;">
                <input type="radio" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input">
                <label class="custom-control-label" :for="item.key" style="margin-top: 5px;">{{ item.value }}</label>
              </div>
              <input v-model="form.others" class="form-control" type="text" placeholder="請填寫" style="width: 175px;">
            </div>
            <div v-else :key="item.key" class="custom-control custom-control-inline custom-radio">
              <input type="radio" v-model="form.shop" :value="item.key" :id="item.key" class="custom-control-input">
              <label :for="item.key" class="custom-control-label">{{ item.value }}</label>
            </div>
          </template>
          <span v-if="errors.shop">
            <small class="text-danger">{{ errors.shop[0] }}</small>
          </span>
        </div>
      </div>
      <div class="d-flex"></div>
      <button class="btn btn-primary btn-block" type="submit" style="margin-top: 15px;">送出</button>
    </form>
  </div>
</template>
<script>
/* global $ */
// import 'jquery-twzipcode'

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
      items: [],
      errors: {}
    }
  },
  methods: {
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
      $('#twzipcode').twzipcode('reset')
    }
  },
  mounted () {
    $('#twzipcode').twzipcode()
  }
}
</script>
