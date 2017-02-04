<template>
  <div id="app">
    <div class="form">
      <input-phone
        :code-phones="codePhones"
        :push-valid-number="pushValidNumber"
      ></input-phone>
    </div>
    <div class="demo-result">
        <span>Demo here valid phone number:</span>
        <div>{{validPhoneNumber}}</div>
    </div>
  </div>
</template>

<script>
import inputPhone from './components/inputPhone'

export default {
  name: 'app',
  components: {
    inputPhone
  },
  data () {
    return {
      validPhoneNumber: 'xxxxxxx',
      codePhones: [
        {
          'name': 'Afghanistan',
          'dial_code': '+93',
          'code': 'AF'
        },
        {
          'name': 'Aland Islands',
          'dial_code': '+358',
          'code': 'AX'
        }
      ]
    }
  },
  methods: {
    pushValidNumber (number) {
      this.validPhoneNumber = number
    }
  }
}
</script>

<style>
#app {
  margin-top: 100px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.form {
  display: inline-block;
  width: 577px;
  height: 100px;
  padding: 12px;
  border: 1px dotted #eee;
  border-radius: 5px;
}

.demo-result {
  display: inline-block;
  width: 577px;
  height: 100px;
  padding: 12px;
}
</style>
