<template lang="pug">

  v-layout(row, wrap)
    v-flex(xs12)
      v-combobox(v-model="selectedCategories", :items="categories", label="Categories", multiple, chips, persistent-hint, hint="The players awarded points will be augmented by the categories.")
        template(v-slot:selection="data")
          v-chip.v-chip--select-multi(:selected="data.selected", :disabled="data.disabled", :color="`${data.item.color} lighten-3`")
            v-avatar.white--text(v-if="(data.item.avatar.length > 0)", :color="data.item.color", v-text="data.item.avatar")
            v-avatar(v-else-if="(data.item.icon.length > 0)", :color="data.item.color")
              v-icon.white--text {{ data.item.icon }}
            span.pr-2 {{ data.item.text }}
            v-icon(small, @click="data.parent.selectItem(data.item)") close
</template>

<script>
export default {
  data: () => ({
    selectedCategories: [],
    categories: [
      {
        id: 1,
        text: "Truth",
        avatar: "",
        icon: "record_voice_over",
        color: "cyan"
      },
      {
        id: 2,
        text: "Alcohol",
        avatar: "",
        icon: "local_bar",
        color: "amber"
      },
      {
        id: 3,
        text: "Stupid",
        avatar: "",
        icon: "healing",
        color: "blue"
      },
      {
        id: 4,
        text: "Expensive",
        avatar: "",
        icon: "attach_money",
        color: "green"
      },
      {
        id: 5,
        text: "Smoking",
        avatar: "",
        icon: "smoking_rooms",
        color: "blue-grey"
      },
      {
        id: 6,
        text: "Humiliation",
        avatar: "H",
        icon: "",
        color: "pink"
      },
      {
        id: 7,
        text: "Photo Evidence",
        avatar: "",
        icon: "camera_alt",
        color: "blue"
      },
      {
        id: 8,
        text: "Adult",
        avatar: "18+",
        icon: "",
        color: "red"
      }
    ]
  }),
  methods: {
    agreed() {
      this.dialog = false;
      this.agree = true;
    },
    disagreed() {
      this.dialog = false;
      this.agree = false;
    }
  }
};
</script>
