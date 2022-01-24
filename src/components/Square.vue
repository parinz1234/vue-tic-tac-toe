<template>
  <button class="square" type="button" @click="onClick">{{ value }}</button>
</template>
<script>
export default {
  name: "Square",
  props: {
    value: {
      type: String,
      default: "",
    },
    onClick: {
      type: Function,
      default: () => {},
    },
  },
  created() {
    console.log(this.onClick);
  },
};
</script>
<style>
.square {
  width: 100px;
  height: 100px;
}
</style>
