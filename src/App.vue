<template>
  <div id="app">
    <div class="ntitle">
      訂閱人事行政總處事求人
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #fefefe;
  color: rgb(15, 82, 82);
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
}

.ntitle {
  font-size: 30px;
  padding: 20px;
  margin: 30px;
  border: 2px solid rgb(15, 82, 82, 0.5);
  border-radius: 30px;
  display: inline-block;
}

.highlight {
  font-size: 28px;
}

html {
  touch-action: manipulation;
}
</style>
