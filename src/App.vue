<template lang="pug">

   v-app
    v-content
      v-container
        v-tabs(fixed-tabs)
          v-tab Create Card
          v-tab-item 
            createCard

          v-tab Decks
          v-tab-item 
            deckDashboard
          
          v-tab Sign Up
          v-tab-item 
            signUp

          v-tab Achievements
          v-tab-item 
            achievements
           
</template>

<script>
import createCard from "./components/cards/CreateCard";
import deckDashboard from "./components/decks/DeckDashboard";
import signUp from "./components/users/SignUp";
import achievements from "./components/users/Achievements";

export default {
  components: {
    createCard,
    deckDashboard,
    signUp,
    achievements
  }
};
</script>

<style>
@import "~vuetify/src/stylus/main";
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>