<template>
  <table>
    <thead>
      <tr>
        <th colspan="6">{{ kanaType }}</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td></td>
        <KanaRowOrColumn :kanas="kanas" letter="a" />
        <KanaRowOrColumn :kanas="kanas" letter="i" />
        <KanaRowOrColumn :kanas="kanas" letter="u" />
        <KanaRowOrColumn :kanas="kanas" letter="e" />
        <KanaRowOrColumn :kanas="kanas" letter="o" />
      </tr>
      <tr>
        <td></td>
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="0" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="1" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="2" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="3" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="4" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="k-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="5" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="6" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="7" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="8" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="9" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="s-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="10" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="11" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="12" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="13" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="14" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="t-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="15" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="16" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="17" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="18" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="19" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="n-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="20" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="21" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="22" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="23" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="24" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="h-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="25" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="26" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="27" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="28" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="29" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="m-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="30" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="31" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="32" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="33" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="34" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="y-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="35" />
        <td></td>
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="36" />
        <td></td>
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="37" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="r-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="38" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="39" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="40" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="41" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="42" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="w-" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="43" />
        <td></td>
        <td></td>
        <td></td>
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="44" />
      </tr>
      <tr>
        <KanaRowOrColumn :kanas="kanas" letter="n" />
        <KanaCell :kanaType="kanaType" :kanas="kanas" :index="45" />
        <td></td>
        <td></td>
        <td></td>
        <td></td>
      </tr>
    </tbody>
  </table>
</template>

<script lang="ts">
  // styled component : https://class-component.vuejs.org/
  import { Component, Prop, Vue } from "vue-property-decorator";
  import KanaCell from "./KanaCell.vue";
  import KanaRowOrColumn from "./KanaRowOrColumn.vue";

  @Component({
    components: {
      KanaCell,
      KanaRowOrColumn,
    },
  })
  // insert data default and methods.
  export default class KanaTable extends Vue {
    @Prop({ default: "Hiragana" })
    kanaType: string;
    @Prop({ default: {} })
    kanas: Reduce<string, any>[];
  }
</script>

<style lang="scss">
  table {
    width: 400px;
    margin-right: 20px;
  }

  td,
  th {
    width: 60px;
    height: 60px;
    font-size: 1.3rem;
    border: 1px solid black;
    cursor: pointer;
    user-select: none;
  }
</style>
