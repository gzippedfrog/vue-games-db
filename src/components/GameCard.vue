<template>
  <v-card class="mx-auto" width="400">
    <v-card-title>
      <div class="v-card__game-name">
        {{ game.name }}
      </div>
      <div :class="`v-card__metascore v-card__metascore_${scoreColor}`">
        {{ game.metacritic }}
      </div>
    </v-card-title>

    <v-card-subtitle>
      {{ releaseDate }}
    </v-card-subtitle>

    <v-carousel v-model="slide" continuous hide-delimiters height="200">
      <v-carousel-item
        v-for="item in game.short_screenshots"
        :src="item.image.replace('/media/', '/media/crop/600/400/')"
        :key="item.id"
      >
      </v-carousel-item>
    </v-carousel>

    <v-card-text>
      <v-chip-group column multiple active-class="primary--text">
        <v-chip v-for="genre in game.genres" :key="genre.id">
          {{ genre.name }}
        </v-chip>
      </v-chip-group>
    </v-card-text>

    <v-card-actions>
      <v-btn color="orange lighten-2" text> More Info </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import moment from "moment";

export default {
  name: "GameCard",
  props: {
    game: Object,
  },
  data: () => ({
    show: true,
    slide: 0,
  }),
  computed: {
    releaseDate() {
      return moment(this.$props.game.released, "YYYY-MM-DD").format(
        "DD MMM YYYY"
      );
    },
    scoreColor() {
      const score = this.$props.game.metacritic;
      if (score >= 70) {
        return "high";
      } else if (score >= 30) {
        return "medium";
      } else {
        return "low";
      }
    },
  },
  mounted() {
    // console.log(this.$props.game.saturated_color);
  },
};
</script>

<style scoped>
.v-card {
  height: 100%;
  display: flex;
  flex-direction: column;
}
.v-card__title {
  flex-wrap: nowrap;
  align-items: flex-start;
  justify-content: space-between;
  gap: 0.5;
  height: 6rem;
  word-break: break-word;
}

.v-card__game-name {
  max-lines: 1;
}

.v-card__metascore {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
  /* border: .5rem solid; */
  border: none;
  border-radius: 0.3rem;
  width: 1.9rem;
  height: 1.9rem;
  font-size: 0.7rem;
  font-weight: bold;
  line-height: 1em;
  color: black;
}

.v-card__metascore_high {
  background-color: #6c3;
}

.v-card__metascore_medium {
  background-color: #fc3;
}

.v-card__metascore_low {
  background-color: #f00;
}

.v-card__actions {
  flex-grow: 1;
  align-items: flex-end;
  justify-content: flex-end;
}
</style>
