<template>
  <div>
    <div class="board-row">
      <square index="0" :value="squares[0]" @clickItem="onClickSqaureItem"></square>
      <square index="1" :value="squares[1]" @clickItem="onClickSqaureItem"></square>
      <square index="2" :value="squares[2]" @clickItem="onClickSqaureItem"></square>
    </div>
    <div class="board-row">
      <square index="3" :value="squares[3]" @clickItem="onClickSqaureItem"></square>
      <square index="4" :value="squares[4]" @clickItem="onClickSqaureItem"></square>
      <square index="5" :value="squares[5]" @clickItem="onClickSqaureItem"></square>
    </div>
    <div class="board-row">
      <square index="6" :value="squares[6]" @clickItem="onClickSqaureItem"></square>
      <square index="7" :value="squares[7]" @clickItem="onClickSqaureItem"></square>
      <square index="8" :value="squares[8]" @clickItem="onClickSqaureItem"></square>
    </div>
  </div>
</template>

<script>
import Square from "./Square.vue";

export default {
  name: "board",
  components: {
    Square
  },
  props: ["squares"],
  methods: {
    onClickSqaureItem(event) {
      this.$emit("clickSquare", event);
    }
  }
};
</script>
