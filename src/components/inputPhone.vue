<template>
  <div class='wrapper-phone'>
    <div class='phone-label'>Phone number</div>
    <div class="wrapper-input" :class="{'error-input': !isValid}">
      <select v-model='selectedCountry'>
        <option v-for='(code, index) in codePhones' :value="code">{{code.code}} {{code.dial_code}}</option>
      </select>
      <input placeholder="066 123 4567"
        v-model='phone'
        @blur="updateData(firstBlur = true)"
        >
      </div>
    <div class='result-phone-validation' :class="{'message': !isValid}">{{message}}</div>
  </div>

</template>
<script>
/* eslint-disable */
export default {
  name: 'inputPhone',
  props: {
    codePhones: Array,
    pushValidNumber: Function,
  },
  data () {
    return {
      phone: '',
      selectedCountry: this.codePhones[0],
      firstBlur: false,
      isValid: true,
    }
  },
  computed: {
    message () {
      return !this.firstBlur ? '' : this.isValid ? 'Valid number' : 'Invalid phone number';
    },
  },
  methods: {
    trimNumber (val) {
      return val.replace(/[^0-9.]/g, '');
    },
    validate (val) {
      return new RegExp('^[0-9\-\+]{9,15}$').test(this.phone);
    },
    updateData () {
      if (!this.firstBlur) {
        console.log(this.phone);
        this.firstBlur = false;
        return '';
      }
      this.isValid = this.validate(this.phone);
      const value = this.isValid ? `${this.selectedCountry.dial_code}${this.phone}` : '';
      console.log('update2', this.isValid);
      this.pushValidNumber(this.trimNumber(value));
    }
  },
  watch: {
    phone () {
      this.updateData ();
    },
    selectedCountry () {
      this.updateData ();
    }
  }
}
</script>

<style scoped>
.wrapper-phone {
  text-align: left;
}

.wrapper-input {
  border-bottom: 1px solid #c5d5e2;
}

.phone-label {
  color: #c5d5e2;
}

.result-phone-validation {
  color: green;
}

.message {
  color: red;
}

.error-input {
  border-bottom: 1px solid red;
}

input, select {
  height: 34px;
  padding: 2px 8px;
  font-size: 16px;
  background: none;
  border: none;
  outline: none;
}

</style>
