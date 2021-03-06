<template>
  <div class="sort-page">
    <h1 style="margin-top: 20px">
      <a href="https://en.wikipedia.org/wiki/Counting_sort">Counting Sort</a>
    </h1>
    <h3>Time complexity O(n + k)</h3>
    <h3>Space complexity O(n + k)</h3>
    <h3 style="margin-bottom: 20px">
      k - range of the non-negative key values
    </h3>
    <div class="stats">
      <v-col>
        <span>{{ this.sketch.compsCounter }} comparisons</span>
        <v-spacer></v-spacer>
        <span v-if="this.sketch.values"
          >N: {{ this.sketch.values.length }}</span
        >
        <v-spacer></v-spacer>
        <span>Steps per second: {{ this.stepsPerSecond }}</span>
      </v-col>
    </div>
    <canvas id="sketch" :width="canvasWidth" :height="canvasHeight"> </canvas>
    <div class="controls">
      <v-col>
        <button
          v-on:click="sketch.setup({ n: n, stepsPerSecond: stepsPerSecond })"
        >
          START
        </button>
        <v-spacer></v-spacer>
        <span style="font-size: large">N: {{ this.n }}</span>
        <v-spacer></v-spacer>
        <input
          style="width: min(100%, 800px)"
          v-model="n"
          type="range"
          min="10"
          max="2000"
          step="10"
        />
        <div style="height: 20px"></div>
        <span style="font-size: large"
          >Steps per second: {{ this.stepsPerSecond }}</span
        >
        <v-spacer></v-spacer>
        <input
          style="width: min(100%, 800px)"
          v-model="stepsPerSecond"
          type="range"
          min="100"
          max="5000"
          step="100"
        />
      </v-col>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { CountingSortSketch } from "../algos/CountingSort";
import { Painter } from "../utilities/painter";

export default Vue.extend({
  name: "CountingSort",
  data: () => ({
    canvasWidth: 2000,
    canvasHeight: 1125,
    sketch: {} as CountingSortSketch,
    n: 100,
    stepsPerSecond: 100,
  }),
  mounted() {
    const canvas = document.getElementById("sketch");
    if (canvas && Painter.isCanvas(canvas)) {
      this.sketch = new CountingSortSketch(canvas);
      this.sketch.setup();
    }
  },
});
</script>

<style>
.sort-page {
  width: max(350px, min(90vw, 1300px));
  margin-left: auto;
  margin-right: auto;
}

.sort-page h1 a {
  color: #ff79c6;
  text-decoration: none;
}
.sort-page h1 a:hover {
  text-decoration: underline;
}
.sort-page h1 a:active {
  color: #8be9fd;
  text-decoration: underline;
}

#sketch {
  width: 100%;
  display: block;
  margin-left: auto;
  margin-right: auto;
  padding: 10px;
  border-radius: 10px;
  border: 3px dashed #bd93f9;
}

.controls button {
  background-color: #ff79c6;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 20px;
  margin-top: 10px;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: block;
  font-size: 17px;
  border-radius: 10px;
}
</style>
