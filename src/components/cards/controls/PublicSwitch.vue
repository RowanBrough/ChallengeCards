<template lang="pug">
  
  v-container.pa-0.ma-0
    v-layout(align-center, justify-center, row)
      div.item(@click.prevent="isPublic = false")
        slot(name="private-text")
          v-btn(fab, :outline="isPublic", color="blue")
            v-icon(:class="(!isPublic ? 'white--text': '')") visibility_off
      div
        v-switch.px-3(v-model="isPublic", color="blue")
      div.item(@click.prevent="isPublic = true")
        slot(name="public-text")
          v-btn(fab, :outline="!isPublic", color="blue")
            v-icon(:class="(isPublic ? 'white--text': '')") visibility
    
    v-layout(align-center, justify-center, row)
      div.v-messages.pt-3
        div.v-messages__wrapper
          div.v-messages__message
            slot(name="hint-private-text", v-if="!isPublic") This card will be set to private. Only you and the players you share it with will be able to interact with it.
            slot(name="hint-public-text", v-if="isPublic") This card will be set to public. Once adudicated by the community it will be added to the main games deck.

    v-dialog(v-model="dialog")
      v-card
        v-card-title(class="headline")
          slot(name="terms-header") Terms and Conditions
        v-card-text
          slot(name="terms-content") Let Goog

</template>

<script>
export default {
  data: () => ({
    isPublic: true,
    dialog: false
  })
};
</script>

