<template>
  <div class="todo-list" :class="mode">
    <Toogle :mode="mode" @toggle="$emit('toggle')"/>
    <h3>To Do List</h3>
    <input
      type="text"
      class="input-new-item"
      v-on:keyup.enter="addNewItemToList"
      placeholder="Adicionar tarefa"
    />

    <ul>
      <ListItem
        v-for="(item, index) in list"
        :key="index"
        :item="item"
        :index="index"
        @delete-item="deleteItem"
      />
    </ul>
  </div>
</template>

<script>
import ListItem from "./ListItem";
import Toogle from './Toogle.vue';

export default {
  name: "TodoList",
  props: ['mode'],
  components: {
    ListItem,
    Toogle
  },
  data() {
    return {
      list: [],
    };
  },
  created() {
    const itemInLocalStorage = JSON.parse(localStorage.getItem("list"));
    this.list = itemInLocalStorage ? itemInLocalStorage : [];
  },
  methods: {
    addNewItemToList(event) {
      const newItem = event.target.value;
      this.list.unshift({
        label: newItem,
        checked: false,
      });
      event.target.value = "";
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    },
    updateLocalStorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
  watch: {
    list() {
      this.updateLocalStorage();
    },
  },
};
</script>

<style>
.todo-list {
  width: 600px;
  margin: auto;
  padding: 20px;
  border-radius: 5px;
  background: var(--light-grey);
  transition: background 0.3s ease-in-out;
}

.dark .todo-list {
  background: var(--light-dark);
}


.todo-list h3 {
  font-size: 30px;
}

.input-new-item {
  width: 80%;
  height: 30px;
  background: transparent;
  color: #2c3e506e;
  font-size: 17px;
  border: 0;
  border-bottom: 2px solid rgba(255, 0, 85, 0.568);
}

.input-new-item:focus {
  color: #2c3e50;
  box-shadow: 0;
  outline: 0;
  border-bottom: 2px solid rgb(255, 0, 85);
}

.dark .todo-list .input-new-item:focus {
  color: var(--medium-grey);
}

ul {
  list-style: none;
  padding: 0;
  width: 80%;
  margin: 20px auto;
  text-align: left;
  font-size: 20px;
}
</style>
