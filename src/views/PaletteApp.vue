<template>
  <h1>Vue パレット</h1>
  <div class="app">
    <div class="palette" style="background-color: rgba(0, 0, 200, 0.5)"></div>
    <p>rgba( {{ 0 }}, {{ 0 }}, 200, 0.5 )</p>
    <div class="colors-container">
      <div class="mini-palette"></div>
    </div>
  </div>
</template>

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
