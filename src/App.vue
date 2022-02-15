<template>
  <div class="app">
    <h1>Rejse Udligning</h1>
    <div class="start" v-show="start">
      <p>Start</p>
    </div>
    <div class="ontheway" v-show="ontheway">
      <p>Undervejs</p>
    </div>
    <div class="end" v-show="end">
      <p>Slut</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  components: {},
  data() {
    return {
      start: true,
      ontheway: false,
      end: false,
    };
  },
});
</script>

<style>
</style>
