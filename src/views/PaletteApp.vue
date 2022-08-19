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
      <div class="main-container">
        <h2>紫</h2>
        <div
          class="mini-palette"
          v-for="color in colorsPurple"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
      <div class="main-container">
        <h2>桃</h2>
        <div
          class="mini-palette"
          v-for="color in colorsPink"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
      <div class="main-container">
        <h2>水</h2>
        <div
          class="mini-palette"
          v-for="color in colorsLightBlue"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
      <div class="main-container">
        <h2>緑</h2>
        <div
          class="mini-palette"
          v-for="color in colorsGreen"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
      <div class="main-container">
        <h2>黄</h2>
        <div
          class="mini-palette"
          v-for="color in colorsYellow"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
      <div class="main-container">
        <h2>淡</h2>
        <div
          class="mini-palette"
          v-for="color in colorsPastel"
          v-bind:key="color"
          v-bind:style="color"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      r: 0,
      g: 0,
      colorsPurple: [],
      colorsPink: [],
      colorsLightBlue: [],
      colorsGreen: [],
      colorsYellow: [],
      colorsPastel: [],
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
      if (this.r <= 170 && this.g <= 127) {
        this.colorsPurple.push(newColor)
      } else if (this.r >= 171 && this.g <= 127) {
        this.colorsPink.push(newColor)
      } else if (this.r <= 127 && this.g >= 128) {
        this.colorsLightBlue.push(newColor)
      } else if (this.r <= 235 && this.g >= 230) {
        this.colorsGreen.push(newColor)
      } else if (this.r >= 236 && this.g >= 230) {
        this.colorsYellow.push(newColor)
      } else {
        this.colorsPastel.push(newColor)
      }
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
  margin: 10px;
  margin-top: 0px;
}

.main-container {
  display: flex;
  flex-direction: column;
  width: 80px;
  margin-left: 10px;
  border: 1px solid black;
  text-align: center;
  margin-top: 10px;
}

.colors-container {
  display: flex;
  flex-wrap: wrap;
  width: 300px;
  padding-top: 8px;
}
</style>
