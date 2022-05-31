<template>
  <MainScreen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <InterractScreen
    v-if="statusMatch === 'match'"
    :cardsContext="this.settings.cardsContext"
    @onFinish="onGetResult"
  />
  <ResultScreen
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="this.statusMatch = 'default'"
  />
  <CoppyRightScreen />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import CoppyRightScreen from "./components/CoppyRightScreen.vue";
import InterractScreen from "./components/InterractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "./utils/array";
export default {
  name: "App",
  data() {
    return {
      settings: {
        totalOfBlocks: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  components: {
    MainScreen,
    CoppyRightScreen,
    InterractScreen,
    ResultScreen,
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlocks = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlocks / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(cards)))
      );
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";
    },

    onGetResult() {
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
  },
};
</script>
