<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
    @getWidthMain="getWidthMain()"
  ></main-screen>
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @endGame="onHandleAfterEndGame()"
    :timeGame="settings.timeGame"
    :widthMain="settings.widthMain"
  ></interact-screen>
  <result-screen
    v-if="statusMatch === 'endGame'"
    @onReStart="onReStart()"
    :timeEndGame="settings.timeEndGame"
  ></result-screen>
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "@/components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "./utils/array.js";
export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
  },
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
        timeGame: "0:00",
        widthMain: null,
        timeEndGame: null,
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(config) {
      this.settings.totalOfBlock = config.totalOfBlock;

      const pathCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );

      const cards = [...pathCards, ...pathCards];
      this.settings.cardsContext = shuffled(cards);
      this.settings.startedAt = new Date().getTime();
      this.statusMatch = "match";

      setInterval(() => {
        this.millisToMinutesAndSeconds(
          new Date().getTime() - this.settings.startedAt
        );
      }, 1000);
    },
    onHandleAfterEndGame() {
      this.statusMatch = "endGame";
      this.settings.timeEndGame = this.settings.timeGame;
      console.log(this.settings.timeEndGame);
    },
    millisToMinutesAndSeconds(millis) {
      var minutes = Math.floor(millis / 60000);
      var seconds = ((millis % 60000) / 1000).toFixed(0);
      this.settings.timeGame =
        minutes + ":" + (seconds < 10 ? "0" : "") + seconds;
    },
    getWidthMain() {
      const countWidth = Math.sqrt(this.settings.cardsContext.length);
      this.settings.widthMain = countWidth * (120 + 16) + "px";
    },
    onRestart() {
      this.statusMatch = "default";
    },
  },
};
</script>
