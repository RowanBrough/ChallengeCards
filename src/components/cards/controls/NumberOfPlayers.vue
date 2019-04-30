<template lang="pug">

  v-layout(row, wrap)

    v-flex(xs12)
      v-flex(xs12)
        div(class="text-xs-left pb-3")
          v-label Number of Players
        div
          v-slider(v-model="players", class="pb-3", :tick-labels="playerTicksLabels", :min="1", :max="5", step="1", 
          ticks="always", thumb-label="always", always-dirty,
          persistent-hint, :hint="numberOfPlayersHint")
            template(v-slot:thumb-label="props")
              span {{ tickLabel(props.value - 1) }}

</template>

<script>
export default {
  data: () => ({
    players: 1,
    playerTicksLabels: ["1", "2", "3", "4", "5+"]
  }),
  computed: {
    numberOfPlayersHint() {
      if (this.players == 1) {
        return `This card is intended for 1 player only. 
        All points or penalties will fall-upon this sole player.`;
      }
      if (this.players > 1) {
        return `This card is intended for more than 1 player. 
        All points will be awarded to players who accepted and completed the challenge. 
        Full penalties to anyone who backs out`;
      }
    }
  },
  methods: {
    tickLabel(val) {
      return this.playerTicksLabels[val];
    }
  }
};
</script>