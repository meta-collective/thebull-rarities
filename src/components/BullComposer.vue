<template>
  <v-img :src="images[0]" v-bind="$attrs">
    <v-img v-for="(im, i) in images" :key="i" :src="im" class="child" />
  </v-img>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    images: Array,
    size: {
      type: Number,
      default: 400,
    },
  },
});
</script>

<style scoped>
.parent {
  position: relative;
  top: 0;
  left: 0;
}
.child {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
