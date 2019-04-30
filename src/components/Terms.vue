<template lang="pug">

  v-layout(row, wrap)
    v-flex(xs12)
      v-checkbox(:value="checked", :checked="checked", @change="$emit('change', $event)")
        template(v-slot:label="")
          slot(name="agree-text") I have read and agree with the
          a(color="primary", dark, @click.stop="dialog = true")
            slot(name="button-text") Terms and Conditions

      v-dialog(v-model="dialog")
        v-card
          v-card-title(class="headline")
            slot(name="terms-header") Terms and Conditions
          v-card-text
            slot(name="terms-content") Let Google help apps determine location. This means sending anonymous location data to Google, even when no apps are running.
          v-card-actions
            v-spacer
            v-btn(color="red darken-1", flat="flat", @click="disagreed") Disagree
            v-btn(color="green darken-1", flat="flat", @click="agreed") Agree
            
</template>

<script>
export default {
  model: {
    prop: "checked",
    event: "change"
  },
  props: {
    checked: Boolean
  },
  data: () => ({
    dialog: false
  }),
  methods: {
    agreed() {
      this.dialog = false;
      this.$emit("change", true);
    },
    disagreed() {
      this.dialog = false;
      this.$emit("change", false);
    }
  }
};
</script>
