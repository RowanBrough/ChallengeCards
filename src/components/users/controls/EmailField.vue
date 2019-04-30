<template lang="pug">

  v-layout(row, wrap)
    v-flex(xs12)
      v-text-field(:rules="[validateEmail]", :counter="emailLength", :label="label", :prepend-icon="icon", :hint="hint", persistent-hint, required, :value="value", @input="$emit('input', $event)")
            
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: ""
    },
    icon: {
      type: String,
      default: "email"
    },
    label: {
      type: String,
      default: "E-mail"
    },
    hint: {
      type: String,
      default:
        "Used for important things like password resets. We promise we wont spam you."
    }
  },
  data: () => ({
    emailLength: 64,
    emailRegex: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
  }),
  methods: {
    validateEmail(text) {
      if (text.length === 0) return "E-mail is required";
      if (text.length > this.emailLength)
        return `Email must be less than ${this.emailLength} characters`;
      if (!this.emailRegex.test(String(text).toLowerCase()))
        return "E-mail must be valid";
      return true;
    }
  }
};
</script>
