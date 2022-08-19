<template>
  <h1>Vue パレット</h1>
  <div class="app">
    <div
      class="palette"
      v-on:mousemove="getPosition"
      v-bind:style="changeColor"
      v-on:click="saveColor"
    ></div>
    <p>rgba( {{ r }}, {{ g }}, 200, 0.5 )</p>
    <div class="colors-container">
      <div
        class="mini-palette"
        v-for="color in colors"
        v-bind:key="color"
        v-bind:style="color"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      r: 0,
      g: 0,
      colors: [],
    }
  },

  methods: {
    getPosition: function (e) {
      this.r = e.offsetX
      this.g = e.offsetY
    },

    saveColor: function () {
      const newColor = {
        backgroundColor: `rgba(${this.r}, ${this.g}, 200, 0.5)`,
      }
      this.colors.push(newColor)
    },
  },

  computed: {
    changeColor: function () {
      return { backgroundColor: `rgba(${this.r}, ${this.g}, 200, 0.5)` }
    },
  },
}
</script>

<style>
.app {
  display: flex;
  width: 100%;
  flex-direction: column;
  align-items: center;
}
.palette {
  width: 255px;
  height: 255px;
}
.mini-palette {
  min-width: 60px;
  height: 60px;
}
.colors-container {
  display: flex;
  flex-wrap: wrap;
  width: 300px;
  padding-top: 8px;
}
</style>
