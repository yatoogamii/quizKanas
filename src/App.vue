<template>
  <div id="app">
    <h1>Quiz kana</h1>
    <section v-if="!gameStarted" class="lobby-container">
      <KanaTable :kanas="kanas.hiragana" kanaType="Hiragana" />
      <KanaTable :kanas="kanas.katakana" kanaType="Katakana" />
      <GameConfig
        @updateGameStarted="updateGameStarted"
        :gameStarted="gameStarted"
        :finalRules="finalRules"
        :kanas="kanas"
      />
    </section>
    <section v-else class="game-container">
      <Game @updateGameStarted="updateGameStarted" :finalRules="finalRules" />
    </section>
  </div>
</template>

<script lang="ts">
  import { Component, Watch, Vue } from "vue-property-decorator";
  import KanaTable from "./components/KanaTable.vue";
  import GameConfig from "./components/GameConfig.vue";
  import Game from "./components/Game.vue";
  import allKanas from "./tools/kanas.json";

  @Component({
    components: {
      KanaTable,
      GameConfig,
      Game,
    },
  })
  export default class App extends Vue {
    kanas = allKanas.kanas;
    gameStarted = false;

    get finalRules() {
      const finalHiragana = this.kanas.hiragana.filter(kana => {
        return kana.activated;
      });
      const finalKatakana = this.kanas.katakana.filter(kana => {
        return kana.activated;
      });
      const kanasList = finalHiragana.concat(finalKatakana);

      return {
        from: "hiragana",
        to: "rōmaji",
        kanasList: kanasList,
        score: 2,
      };
    }

    updateGameStarted(value: boolean) {
      this.gameStarted = value;
    }

    @Watch("gameStarted")
    onPropertyChanged(value: boolean, oldValue: boolean) {
      if (value === true) {
        const arr = [];

        do {
          arr.push(...this.finalRules.kanasList);
        } while (arr.length < this.finalRules.score);

        // shuffle
        for (let i = arr.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [arr[i], arr[j]] = [arr[j], arr[i]];
        }

        while (arr.length > this.finalRules.score) {
          arr.pop();
        }

        this.finalRules.kanasList = arr;
      } else {
        this.kanas.hiragana.forEach(kana => {
          kana.activated = null;
        });
        this.kanas.katakana.forEach(kana => {
          kana.activated = null;
        });
      }
    }
  }
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .lobby-container {
    width: 90%;
    margin: auto;
    display: flex;
    justify-content: center;
  }

  .game-container {
    width: 90%;
    height: 70vh;
    margin: auto;
    display: flex;
    justify-content: center;
  }
</style>
