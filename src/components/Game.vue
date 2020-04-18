<template>
  <div class="game-overlay">
    <div class="score-container">
      <p>{{ step }} / {{ finalRules.score }}</p>
      <p>score: {{ score }} / {{ finalRules.score }}</p>
    </div>
    <p class="question">
      {{ allQuestions[allQuestions.length - 1][finalRules.from] }}
    </p>
    <input v-model="answer" type="text" value="" name="answer" id="answer" />
    <button @click="validatedAnswer">valider</button>
    <button @click="skipQuestion">passer</button>
  </div>
</template>

<script lang="ts">
  import { Component, Watch, Prop, Vue } from "vue-property-decorator";

  @Component
  export default class Game extends Vue {
    @Prop()
    finalRules: Reduce<string, any>[];

    step = 1;
    score = this.finalRules.score;
    allQuestions = this.finalRules.kanasList;
    answer = "";

    validatedAnswer() {
      if (
        this.answer ===
        this.allQuestions[this.allQuestions.length - 1][this.finalRules.to]
      ) {
        console.log("good");
        this.allQuestions.pop();
      } else {
        console.log("wrong");
        this.score -= 1;
        this.allQuestions.pop();
      }
      this.step += 1;
      this.answer = "";
    }

    skipQuestion() {
      this.allQuestions.pop();
      this.score -= 1;
      this.step += 1;
      this.answer = "";
    }

    @Watch("allQuestions")
    onPropertyChanged(value: any[], oldValue: any[]) {
      if (value.length === 0) {
        const wantRetry = confirm("Voulez vous recommener ?");
        console.log(wantRetry);
        if (wantRetry) {
          this.step = 1;
          this.score = this.finalRules.score;
          this.allQuestions = this.finalRules.kanasList;
        } else {
          this.$emit("updateGameStarted", false);
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .game-overlay {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
  }

  button {
    margin-top: 10px;
  }

  .score-container {
    display: flex;
    justify-content: space-between;
    width: 200px;
  }

  .question {
    font-size: 5rem;
  }
</style>
