<template>
  <div>
    <b-form @submit.prevent="onSubmit" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          v-validate="'required|email'"
          type="email"
          name="email"
          placeholder="Enter email"
        ></b-form-input>
        <span v-show="errors.has('email')" class="form-control-feedback">{{
          errors.first('email')
        }}</span>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Your Password:"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="form.password"
          type="password"
          required
          placeholder="Enter Password"
        ></b-form-input>
      </b-form-group>

      <vue-recaptcha
        ref="invisibleRecaptcha"
        :loadRecaptchaScript="true"
        :sitekey="sitekey"
        @verify="onVerify"
        @expired="onExpired"
        size="invisible"
      ></vue-recaptcha>
      <b-button type="submit" variant="primary">Submit</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
import captcha from 'vue-recaptcha'

export default {
  layout: 'frontlayout',
  components: {
    'vue-recaptcha': captcha
  },
  data() {
    return {
      form: {
        email: '',
        password: '',
        token: ''
      },
      sitekey: process.env.NUXT_ENV_GOOGLE_SITE_KEY,
      show: true
    }
  },

  methods: {
    onSubmit() {
      this.$refs.invisibleRecaptcha.execute()
      this.$validator
        .validateAll()
        .then((x) => {
          console.log(x)
        })
        .catch((e) => {
          console.log(e)
        })
    },
    onVerify(response) {
      this.form.token = response
    },
    onExpired() {
      console.log('Expired')
    },
    resetRecaptcha() {
      this.$refs.recaptcha.reset() // Direct call reset method
    }
  }
}
</script>
