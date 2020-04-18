<template>
  <td
    @click="updateKanas"
    v-bind:class="[
      kanas[index]['activated'] === null
        ? ''
        : kanas[index]['activated'] === true
        ? 'text-green'
        : 'text-red',
    ]"
  >
    {{ kanas[index][kanaType === "Hiragana" ? "hiragana" : "katakana"] }}
    <br />
    {{ kanas[index]["rōmaji"] }}
  </td>
</template>

<script lang="ts">
  import { Component, Prop, Vue } from "vue-property-decorator";

  @Component
  export default class KanaCell extends Vue {
    @Prop({ default: "Hiragana" })
    kanaType: string;
    @Prop({ default: 0 })
    index: number;
    @Prop({ default: {} })
    kanas: Reduce<string, any>[];

    updateKanas() {
      switch (this.kanas[this.index]["activated"]) {
        case null:
          this.kanas[this.index]["activated"] = true;
          break;
        case true:
          this.kanas[this.index]["activated"] = false;
          break;
        case false:
          this.kanas[this.index]["activated"] = null;
          break;
      }
    }
  }
</script>

<style lang="scss">
  .text-green {
    color: green;
  }
  .text-red {
    color: red;
  }
</style>
