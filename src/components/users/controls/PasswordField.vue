<template lang="pug">

  v-layout(row, wrap)
    v-flex(xs12 md6)
      v-text-field(:append-icon="show1 ? 'visibility' : 'visibility_off'", :rules="[validatePassword1]", :type="show1 ? 'text' : 'password'", label="Password", required, :counter="passwordLength", @click:append="show1 = !show1", prepend-icon="lock", :value="value", @input="updatePassword1")
      
    v-flex(xs12 md6)
      v-text-field(v-model="password2", :append-icon="show2 ? 'visibility' : 'visibility_off'", :rules="[validatePassword2]", :type="show2 ? 'text' : 'password'", label="Confirm Password", required, :counter="passwordLength", @click:append="show2 = !show2", prepend-icon=" ")
            
</template>

<script>
export default {
  model: {
    prop: "value",
    event: "input"
  },
  props: {
    value: {
      type: String,
      default: ""
    },
    passwordLength: {
      type: Number,
      default: 30
    }
  },
  data: () => ({
    password1: "",
    password2: "",
    show1: false,
    show2: false
  }),
  methods: {
    updatePassword1(val) {
      this.password1 = val;
      this.$emit("input", val);
    },
    validatePassword1(password) {
      if (password.length === 0) return "Password is required";
      if (password.length > this.passwordLength)
        return `Password must be less than ${this.passwordLength} characters`;
      return true;
    },
    validatePassword2(password) {
      let validPassword = this.validatePassword1(password);
      if (validPassword === true) {
        if (password != this.password1) return "Your passwords don't match.";
      }
      return validPassword;
    }
  }
};
</script>
