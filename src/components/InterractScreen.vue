<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 64) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 + 16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <CardItemFlip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :cardsContext="cardsContext"
        :card="{ index, value: card }"
        @onFlip="checkRule($event)"
      />
    </div>
  </div>
</template>

<script>
import CardItemFlip from "./CardItem.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardItemFlip,
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) {
        return false;
      }
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        this.$refs[`card-${this.rules[0].index}`][0].isDisable = true;
        this.$refs[`card-${this.rules[1].index}`][0].isDisable = true;
        this.rules = [];
        const disabledElements = document.querySelectorAll(
          `.screen .card.is-disable`
        );
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 600);
      } else {
        return false;
      }
    },
  },
};
</script>

<style lang="css">
.screen__inner {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
