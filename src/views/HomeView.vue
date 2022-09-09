<template>
  <v-container >
    <v-row dense>
      <v-col  cols="12" sm="6" md="3" lg="2" v-for="game in data.results" :key="game.id">
        <GameCard :game="game" />
        <!-- <GameCard :game="data.results[4]" /> -->
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import GameCard from "@/components/GameCard.vue";
import data from "@/mock_data/results.json";

export default {
  name: "HomeView",
  components: {
    GameCard,
  },
  data() {
    return {
      data,
    };
  },
};
</script>
