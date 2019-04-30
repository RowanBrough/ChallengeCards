<template lang="pug">

  v-form(ref="signupForm")
    v-layout(row, wrap)
      v-flex(xs12)
        h1 Sign Up
    
      v-flex(xs12)
        EmailField(v-model="email")

      v-flex(xs12)
        BirthdateField(v-model="birthdate")
       
      v-flex(xs12)
        v-text-field(v-model="username", :rules="[validateUsername]", :counter="usernameLength", label="Username", required, prepend-icon="face", hint="This is your display name in game.", persistent-hint)

      v-flex(xs12)
        PasswordField(v-model="password")

      v-flex(xs12)
        Terms(v-model="agreedToTerms")

      v-flex(xs12, v-if="!agreedToTerms && signUpClickCount > 0")
        v-alert.text-xs-left(:value="true", type="warning") Please agree to the terms and conditions.
      
      v-flex(xs12)
        v-btn.white--text(block, color="blue", @click.prevent="SignUp") Sign Up
            
</template>

<script>
import EmailField from "./controls/EmailField";
import BirthdateField from "./controls/BirthdateField";
import PasswordField from "./controls/PasswordField";
import Terms from "../Terms";

export default {
  components: {
    EmailField,
    BirthdateField,
    PasswordField,
    Terms
  },
  data: () => ({
    email: "",
    birthdate: "",
    usernameLength: 50,
    username: "",
    password: "",
    agreedToTerms: false,
    signUpClickCount: 0
  }),
  methods: {
    validateUsername(username) {
      if (username.length === 0) return "Username is required";
      if (username.length > this.usernameLength)
        return `Username must be less than ${this.usernameLength} characters`;
      return true;
    },

    resetValidation() {
      this.$refs.signupForm.resetValidation();
    },

    SignUp() {
      this.signUpClickCount++;
      console.log(this.agreedToTerms, this.password, this.birthdate);
      if (this.$refs.signupForm.validate() && this.agreedToTerms) {
        alert("NICE!");
      }
    }
  }
};
</script>
