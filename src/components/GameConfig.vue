<template>
  <section class="game-config-container">
    <h2>Game config</h2>
    <div class="input-container">
      <label for="allHiragana">all hiragana</label>
      <input
        @change="updateHiragana"
        v-model="hira"
        type="checkbox"
        name="allHiragana"
        id="allHiragana"
      />
    </div>
    <div class="input-container">
      <label for="allKatakana">all katakana</label>
      <input
        @change="updateKatakana"
        v-model="kata"
        type="checkbox"
        name="allKatakana"
        id="allKatakana"
      />
    </div>
    <div class="select-container">
      <label for="from">De</label>
      <select @change="updateFrom" v-model="from" name="from" id="from">
        <option value="hiragana">Hiragana</option>
        <option value="katakana">Katakana</option>
        <option value="rōmaji">Rōmaji</option>
      </select>
    </div>
    <div class="select-container">
      <label for="to">Vers</label>
      <select @change="updateTo" v-model="to" name="to" id="to">
        <option value="hiragana">Hiragana</option>
        <option value="katakana">Katakana</option>
        <option value="rōmaji">Rōmaji</option>
      </select>
    </div>
    <div class="number-container">
      <label for="score">score</label>
      <input
        required
        @input="updateScore"
        v-model="score"
        type="number"
        name="score"
        id="score"
        min="2"
      />
    </div>
    <div class="input-container">
      <button @click="startGame">start quiz</button>
    </div>
  </section>
</template>

<script lang="ts">
  import { Component, Prop, Vue } from "vue-property-decorator";

  @Component
  export default class GameConfig extends Vue {
    // props
    @Prop({ default: {} })
    kanas: Record<string, any>;
    @Prop({ default: {} })
    finalRules: Record<string, any>;
    @Prop({ default: false })
    gameStarted: boolean;

    // data
    hira = false;
    kata = false;
    from = "hiragana";
    to = "rōmaji";
    score = 2;

    updateHiragana() {
      if (this.hira) {
        this.kanas.hiragana.forEach(kana => {
          kana.activated = true;
        });
      } else {
        this.kanas.hiragana.forEach(kana => {
          kana.activated = null;
        });
      }
    }

    updateKatakana() {
      if (this.kata) {
        this.kanas.katakana.forEach(kana => {
          kana.activated = true;
        });
      } else {
        this.kanas.katakana.forEach(kana => {
          kana.activated = null;
        });
      }
    }

    updateScore() {
      this.finalRules.score = Number(this.score);
    }

    updateFrom() {
      this.finalRules.from = this.from;
    }

    updateTo() {
      this.finalRules.to = this.to;
    }

    startGame() {
      if (this.finalRules.kanasList.length <= 1) {
        alert("Veuillez mettre au moins 2 kana");
      } else if (this.finalRules.score <= 1) {
        alert("Veuillez mettre au minimum 2 de score");
      } else {
        this.$emit("updateGameStarted", true);
      }
    }
  }
</script>

<style lang="scss">
  .game-config-container {
    border: 1px solid black;
    width: 400px;
    min-width: 400px;
  }

  h2 {
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .input-container {
    width: 130px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5px;
    padding: 5px;
  }

  .select-container {
    width: 150px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5px;
    padding: 5px;
  }

  .number-container {
    width: 280px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin: 5px;
    padding: 5px;
  }
</style>
