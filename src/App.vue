<template>
  <div id="app">
    <!-- <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav> -->
    <div class="title">
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


.title {
  font-size: 22px;
  padding: 20px;
}

.highlight {
  font-size: 28px;
}

html {
  touch-action: manipulation;
}
</style>
