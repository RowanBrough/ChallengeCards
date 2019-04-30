<template lang="pug">

  v-layout(row, wrap)

    v-flex(xs12)
      h1 Decks

    v-flex(xs12)
      v-container.ma-0.pa-0(fluid, grid-list-md)
        v-layout(row, wrap)
          template(v-for="deck in orderedDecks")
            v-flex(xs12, sm6, md4, lg3)
              v-hover
                v-card(slot-scope="{ hover }", :class="`elevation-${hover ? 12 : 2}`")
                  v-card-title
                    h4 {{ deck.name }}
                  v-divider
                  v-card-text {{ truncate(deck.description) }}
                  v-card-actions
                    v-layout(row, justify-end)
                      v-btn(fab, small)
                        v-icon(v-if="deck.isFavorite") favorite
                        v-icon(v-else) favorite_border

                      v-badge(right)
                        span(slot="badge", v-if="deck.shares > 0") {{deck.shares}}
                        v-btn(fab, small)
                          v-icon share
                      
                      v-badge(right)
                        span(slot="badge", v-if="deck.votes > 0") {{deck.votes}}
                        v-btn(fab, small)
                          v-icon thumb_up
                  v-progress-linear(:value="calculateProgress(deck.votes)", :color="calculateProgressColor(deck.votes)")
                      
</template>

<script>
import _ from "lodash";
export default {
  components: {},
  data: () => ({
    truncateLength: 50,
    decks: [
      {
        id: "512d8b40-65ed-45a0-815a-729bc6ac596b",
        name: "occaecat",
        description:
          "Id magna enim proident exercitation ad est. Qui consequat labore quis in esse ad sunt quis aliquip commodo tempor irure duis aliquip. Et sunt dolore mollit ad dolore excepteur in proident dolore aliquip irure aliquip. Nostrud esse aliquip fugiat aute. Officia eu dolore ipsum proident elit amet nulla nisi nostrud exercitation duis cupidatat fugiat cupidatat.",
        isActive: true,
        isFavorite: true,
        createdBy: {
          id: "24751a0c-d9e0-4f65-b17c-1a4495161ae1",
          username: "Karyn"
        },
        shares: 31,
        votes: 8,
        hasSuggestions: false
      },
      {
        id: "3932f2af-7905-410d-a9ee-6815ab7b24bc",
        name: "fugiat",
        description:
          "Ipsum dolore culpa qui reprehenderit fugiat elit consectetur minim pariatur enim in. In laboris sunt enim minim enim consectetur cillum sunt laboris exercitation sint pariatur. Commodo qui cillum eu do elit laboris. Cupidatat fugiat Lorem veniam consectetur anim esse quis occaecat labore nostrud duis duis consequat reprehenderit. Esse sunt elit in nisi non ut quis.",
        isActive: true,
        isFavorite: false,
        createdBy: {
          id: "9b96d9f9-3b92-4469-8ee6-b16bb52e564c",
          username: "Barlow"
        },
        shares: 19,
        votes: 5,
        hasSuggestions: false
      },
      {
        id: "e2d4242c-45a1-4b6d-a6cd-20fe82f9f265",
        name: "ullamco",
        description:
          "Esse voluptate mollit sunt qui. Duis pariatur laborum aute pariatur ipsum mollit. Cillum aute mollit ex eiusmod est occaecat occaecat aute id officia exercitation. Sit cillum adipisicing magna amet aliquip. Esse quis laborum laboris amet mollit esse occaecat duis anim consequat irure duis non anim.",
        isActive: false,
        isFavorite: true,
        createdBy: {
          id: "94893bc1-717c-491e-bb8d-1c1ba4f93b63",
          username: "Langley"
        },
        shares: 45,
        votes: 6,
        hasSuggestions: false
      },
      {
        id: "d54279f4-741d-4a31-8579-754f213e79c6",
        name: "pariatur",
        description:
          "Labore proident deserunt tempor minim pariatur consequat velit do. Magna ipsum esse excepteur labore mollit sunt aute qui quis. Cupidatat consequat esse proident irure reprehenderit et sunt elit adipisicing voluptate aute cupidatat mollit amet. Qui eu sint cupidatat qui sit nostrud exercitation do non veniam laboris. Ipsum occaecat nisi est aute irure pariatur Lorem quis fugiat ullamco est occaecat aliqua.",
        isActive: true,
        isFavorite: true,
        createdBy: {
          id: "072d6c8f-2036-445e-9d04-911593a7d131",
          username: "Bowen"
        },
        shares: 34,
        votes: 9,
        hasSuggestions: true
      },
      {
        id: "a25cc8de-7d7a-465c-8463-f0b97bd896ed",
        name: "incididunt",
        description:
          "Sit cupidatat nostrud duis consectetur eu minim. Occaecat fugiat pariatur amet incididunt. Et Lorem deserunt nisi cillum velit qui id. Labore minim enim velit ad velit amet reprehenderit est veniam sit nostrud enim ut pariatur. Sunt ea quis officia qui cillum dolore.",
        isActive: true,
        isFavorite: false,
        createdBy: {
          id: "d44572da-4621-4721-a8c3-bef786e8f37a",
          username: "Justice"
        },
        shares: 5,
        votes: 1,
        hasSuggestions: true
      }
    ]
  }),
  computed: {
    orderedDecks() {
      return _.orderBy(this.decks, "isFavorite", ["desc"]);
    }
  },
  methods: {
    truncate(text) {
      if (text.length > this.truncateLength)
        return text.substring(0, this.truncateLength - 3) + "...";
      return text;
    },
    calculateProgress(votes) {
      return votes * 10;
    },
    calculateProgressColor(votes) {
      if (votes >= 10) return "green";
      if (6 < votes && votes <= 9) return "yellow";
      if (3 < votes && votes <= 6) return "orange";
      if (votes <= 3) return "red";
    }
  }
};
</script>

<style scoped>
</style>

