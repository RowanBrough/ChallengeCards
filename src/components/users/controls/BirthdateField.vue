<template lang="pug">

  v-layout(row, wrap)
    v-flex(xs12)
      v-dialog(ref="birthdateDialog", v-model="birthdateModal", :return-value.sync="birthdate", persistent, lazy, full-width, width="290px")
        template(v-slot:activator="{ on }")
          v-text-field(label="Birthdate", ref="birthdateInput" prepend-icon="event", readonly, required, clearable, v-on="on", :rules="[validateBirthdate]", :hint="ageHint", persistent-hint, :value="value", @input="updateBirthdate")
        v-date-picker(v-model="birthdate", ref="birthdatePicker" no-title, scrollable, :min="minBirthdate", :max="maxBirthdate")
          v-spacer
          v-btn(flat, color="primary", @click="cancelBirthdateDialog") Cancel
          v-btn(flat, color="primary", @click="acceptBirthdateDialog") OK
            
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
    minBirthdate: {
      type: String,
      default: "1930-01-01"
    },
    maxBirthdate: {
      type: String,
      default: new Date().toISOString().substr(0, 10)
    },
    yearsToMinus: {
      type: Number,
      default: 18
    }
  },
  data: () => ({
    birthdate: "",
    birthdateModal: false,
    age: null
  }),
  computed: {
    ageHint() {
      if (this.age && this.age > 0) {
        return `You are ${this.age} years old.`;
      }
      return "Please select an age";
    }
  },
  methods: {
    updateBirthdate(val) {
      this.birthdate = val;
      this.$emit("input", val);
    },
    validateBirthdate(birthdate) {
      if (
        this.birthdate === null ||
        this.birthdate === undefined ||
        birthdate.length === 0
      )
        return "Birthdate is required";
      return true;
    },

    cancelBirthdateDialog() {
      this.birthdate = null;
      this.$refs.birthdateDialog.save(this.birthdate);
      this.updateBirthdate(this.birthdate);
    },

    acceptBirthdateDialog() {
      let selectedDate = new Date(this.birthdate);

      let date = new Date();
      date.setFullYear(date.getFullYear() - selectedDate.getFullYear());
      this.age = date.getFullYear();

      this.$refs.birthdateDialog.save(this.birthdate);
      this.updateBirthdate(this.birthdate);
    }
  },
  watch: {
    birthdateModal(val) {
      if (val && this.birthdate === "") {
        let date = new Date();
        date.setFullYear(date.getFullYear() - this.yearsToMinus);
        this.birthdate = date.toISOString().substr(0, 10);
      }
      val &&
        setTimeout(() => (this.$refs.birthdatePicker.activePicker = "YEAR"));
    }
  }
};
</script>
