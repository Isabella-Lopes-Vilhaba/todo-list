<template>
  <div class="app" :class="mode">
    <div id="app">
      <TodoList :mode="mode" @toggle="toggle"/>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  data() {
    return {
      mode: 'light'
    }
  },
  components: {
    TodoList
  },
  methods: {
    toggle () {
      if (this.mode === "dark") {
        this.mode = "light";
      } else {
        this.mode = "dark";
      }
    }
  }
}
</script>

<style>
:root {
  --text-dark: #2c3e50;
  --light-dark: #2e4153;
  --dark: rgb(22, 32, 44);
  --light-grey: rgb(247, 247, 247);
  --medium-grey: rgb(238, 238, 238);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  width: 100vw;
  min-height: 100vh;
  background: var(--medium-grey);
  color: var(--text-dark);
  padding: 60px;
  transition: background 0.3s ease-in-out;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.dark {
  background: var(--dark);
  color: var(--medium-grey);
}
</style>
