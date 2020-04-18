<template>
  <th @click="updateKanas">{{ letter }}</th>
</template>

<script lang="ts">
  import { Component, Prop, Vue } from "vue-property-decorator";

  @Component
  export default class KanaRowOrColumn extends Vue {
    @Prop()
    letter: string;
    @Prop()
    kanas: Reduce<string, any>[];

    updateKanas() {
      switch (this.letter) {
        case "s-":
          this.kanas.forEach(kana => {
            if (
              (kana["rōmaji"].includes(this.letter[0]) ||
                kana["rōmaji"].includes("shi")) &&
              !kana["rōmaji"].includes("tsu")
            ) {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
          break;
        case "t-":
          this.kanas.forEach(kana => {
            if (
              kana["rōmaji"].includes(this.letter[0]) ||
              kana["rōmaji"].includes("chi") ||
              kana["rōmaji"].includes("tsu")
            ) {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
          break;
        case "h-":
          this.kanas.forEach(kana => {
            if (
              (kana["rōmaji"].includes(this.letter[0]) ||
                kana["rōmaji"].includes("fu")) &&
              !kana["rōmaji"].includes("chi") &&
              !kana["rōmaji"].includes("shi")
            ) {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
          break;
        case "n-":
          this.kanas.forEach(kana => {
            if (
              kana["rōmaji"].includes(this.letter[0]) &&
              kana["rōmaji"] !== "n"
            ) {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
          break;
        case "n":
          this.kanas.forEach(kana => {
            if (kana["rōmaji"] === "n") {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
          break;

        default:
          this.kanas.forEach(kana => {
            if (kana["rōmaji"].includes(this.letter[0])) {
              kana.activated === null
                ? (kana.activated = true)
                : kana.activated === true
                ? (kana.activated = false)
                : (kana.activated = null);
            }
          });
      }
    }
  }
</script>

<style lang="scss"></style>
