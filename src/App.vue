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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  width: 100vw;
  min-height: 100vh;
  background: rgb(238, 238, 238);
  color: #2c3e50;
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
  background: rgb(22, 32, 44);
  color: rgb(238, 238, 238);
}
</style>
