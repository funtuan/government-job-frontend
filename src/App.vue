<template>
  <div id="app">
    <div class="ntitle">
      <span class="highlight">
        訂閱
      </span>
      人事行政總處事求人
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
  margin: 20px;
}

.highlight {
  background: #08a50d;
  color: #fff;
  border-radius: 10px;
  padding: 5px 10px;
  display: inline-block;
}

html {
  touch-action: manipulation;
}
</style>
