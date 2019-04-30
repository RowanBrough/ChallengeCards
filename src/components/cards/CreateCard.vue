<template lang="pug">

   v-form(v-model="valid")
      v-layout(row, wrap)

        v-flex(xs12)
          h1 Custom Challenge Card
        
        v-flex(xs12)
          v-textarea(v-model="challenge", auto-grow, label="Challenge", required, persistent-hint, clearable, rows="1" 
          hint="The player will be challenged to do this.")

        v-flex(xs12)
          div.text-xs-left.pb-3
            v-label Severity
          div
            v-slider(v-model="severity", :color="color", thumb-label="always", always-dirty, min="1", max="100", persistent-hint,
            hint="The player is awarded points based on this severity number.")

        v-flex(xs12)
          CategoryDropdown

        v-flex(xs12)
          NumberOfPlayers

        v-flex(xs12)
          PublicSwitch

        v-flex(xs12)
          Terms(v-model="agreedToTerms")

        v-flex(xs12)
          v-btn.white--text(block, color="blue") Save Challenge Card

</template>

<script>
import CategoryDropdown from "./controls/CategoryDropdown";
import NumberOfPlayers from "./controls/NumberOfPlayers";
import PublicSwitch from "./controls/PublicSwitch";
import Terms from "../Terms";

export default {
  components: {
    CategoryDropdown,
    NumberOfPlayers,
    PublicSwitch,
    Terms
  },
  data: () => ({
    valid: false,
    challenge: "",
    severity: 1,
    agreedToTerms: false
  }),
  computed: {
    color() {
      if (this.severity < 25) return "green";
      if (this.severity < 50) return "amber";
      if (this.severity < 75) return "orange";
      return "red";
    }
  },
  methods: {}
};
</script>
