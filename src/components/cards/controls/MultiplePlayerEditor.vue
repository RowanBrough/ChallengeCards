<template lang="pug">

  v-layout.multiple-player-editor(row, wrap)

      v-flex(xs12, sm6)
        v-switch.blue.darken-2(v-model="multiplePlayers", :label="(multiplePlayers?'Multiple Player Challenge':'Single Player Challenge')", persistent-hint,
            :hint="(multiplePlayers? 'Allows the player to add multiple players to partake in the challenge with them.' : 'This challenge can only be undertaken by one player.')")
          
      v-flex(xs12, sm6, v-if="multiplePlayers")
        v-layout(row, wrap)
          v-flex(xs12)
            v-slider.pb-3(v-model="players", :tick-labels="playerTicksLabels", :min="1", :max="4", step="1", ticks="always", persistent-hint, hint="The added players will be awarded percentage of the challenge points.")
          
          v-flex(xs12)
            v-layout(row, wrap)
              v-flex(xs12)
                v-slider.pa-1(v-if="players >= 1 && players != 4", ref="slider1", v-model="slider1Value", :min="1", :max="100", thumb-label="always", always-dirty, append-icon="person", @change="sliderValueChange($event, 1)")
                
                v-btn(v-if="players >= 2 && players != 4", flat, icon, :color="(slider2Linked ? 'blue darken-2' : 'red darken-2')", @click="slider2Linked = !slider2Linked")
                  v-icon {{ (slider2Linked ? 'link' : 'link_off') }}
                v-slider.pa-1(v-if="players >= 2 && players != 4", ref="slider2", v-model="slider2Value", :min="1", :max="100", thumb-label="always", always-dirty, append-icon="person", @change="sliderValueChange($event, 2)")
                
                v-btn(v-if="players >= 3 && players != 4", flat, icon, :color="(slider3Linked ? 'blue darken-2' : 'red darken-2')", @click="slider3Linked = !slider3Linked")
                  v-icon {{ (slider3Linked ? 'link' : 'link_off') }}
                v-slider.pa-1(v-if="players >= 3 && players != 4", ref="slider3", v-model="slider3Value", :min="1", :max="100", thumb-label="always", always-dirty, append-icon="person", @change="sliderValueChange($event, 3)")

                v-slider.pa-1(v-if="players === 4", ref="slider4", v-model="slider4Value", :min="1", :max="100", thumb-label="always", always-dirty, append-icon="people")

</template>

<script>
export default {
  data: () => ({
    multiplePlayers: false,
    players: 1,
    playerTicksLabels: ["1", "2", "3", "4+"],
    slider1Value: 1,
    slider2Value: 1,
    slider3Value: 1,
    slider4Value: 1,
    slider2Linked: true,
    slider3Linked: true
  }),
  computed: {
    loopPlayers() {
      if (this.players >= 4) return 1;
      else return this.players;
    }
  },
  methods: {
    toggleLinked(val) {
      const isFound = this.isIndexInArray(val);
      if (isFound) {
        const index = this.getIndexInArray(val);
        this.unlinked.splice(index, 1);
      } else {
        this.unlinked.push(parseInt(val));
      }
    },
    isIndexInArray(index) {
      return this.getIndexInArray(index) != -1;
    },
    getIndexInArray(index) {
      if (this.unlinked.length > 0) {
        return this.unlinked.findIndex(val => val === index);
      }
      return -1;
    },

    sliderValueChange(val, index) {
      if (index === 1) {
        if (this.slider2Linked) this.slider2Value = val;
        if (this.slider3Linked) this.slider3Value = val;
      } else if (index === 2 && this.slider2Linked) {
        this.slider1Value = val;
        if (this.slider3Linked) this.slider3Value = val;
      } else if (index === 3 && this.slider3Linked) {
        this.slider1Value = val;
        if (this.slider2Linked) this.slider2Value = val;
      }
    }
  }
};
</script>

<style>
.multiple-player-editor .v-slider__thumb-label span::after {
  display: inline-block;
  content: "%";
}
</style>
