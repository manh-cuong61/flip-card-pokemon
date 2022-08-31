<template>
  <div class="screen">
    <h1>Interact component here...</h1>
    <h3>{{ timeGame }}</h3>
    <div class="main" :style="{ width: widthMain }">
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imageBackFaceUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        @onFlip="checkRule($event)"
      ></card-flip>
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  components: {
    CardFlip,
  },
  props: {
    cardsContext: {
      type: Array,
      default: () => [],
    },
    timeGame: {
      type: String,
    },
    widthMain: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      rules: [],
      allRules: [],
    };
  },
  methods: {
    checkRule(card) {
      this.rules.push(card);
      if (this.rules.length === 2) {
        this.allRules.push(this.rules);
        this.rules = [];
      }
      this.allRules.forEach((rule) => {
        if (rule[0].value == rule[1].value) {
          this.$refs[`card-${rule[0].index}`][0].onEnabledDisabledMode();
          this.$refs[`card-${rule[1].index}`][0].onEnabledDisabledMode();
          const cardDisable = document.querySelectorAll(".card.disabled");
          console.log(this.cardsContext.length, cardDisable.length);
          if (this.cardsContext.length == cardDisable.length + 2) {
            this.$emit("endGame");
          }
        } else {
          setTimeout(() => {
            this.$refs[`card-${rule[0].index}`][0].onFlipBackCard();
            this.$refs[`card-${rule[1].index}`][0].onFlipBackCard();
          }, 800);
        }
      });
      this.allRules = [];
    },
  },
};
</script>
<style scoped>
.screen {
  position: absolute;
  top: 5%;
  left: 50%;
  transform: translateX(-50%);
}
.screen h3,
h1,
.actions,
.main {
  text-align: center;
}
.screen h3 {
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>
