<template>
  <section class="real-app">
    <input
      type="text"
      class="add-input"
      autofocus="autofocus"
      placeholder="接下去要做什么？"
      @keyup.enter="addtodo"
    >
    <Item v-for="todo in todosShow" :key="todo.id" :todoValue="todo" @del="deleteFun"/>
    <Tabs :filter="filter" :todos="todos" @filterToggle="filterFun" @clear="clearCompleted"/>
  </section>
</template>

<script>
import Item from "./item.vue";
import Tabs from "./tabs.vue";
let id = 0;
export default {
  data() {
    return {
      todos: [],
      filter: 'all'
    };
  },
  components: {
    Item,
    Tabs
  },
  computed: {
    todosShow() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "active") {
        return this.todos.filter(item => !item.completed);
      }
      if (this.filter === "completed") {
        return this.todos.filter(item => item.completed);
      }
    }
  },
  methods: {
    addtodo(e) {
      if (e.target.value.trim() !== "") {
        this.todos.unshift({
          id: id++,
          content: e.target.value.trim(),
          completed: false
        });
      }
      e.target.value = ''
    },
    deleteFun(id) {
      this.todos.splice(this.todos.findIndex(item => item.id === id), 1)
    },
    filterFun(state) {
      this.filter = state
    },
    clearCompleted() {
      this.todos = this.todos.filter(item => !item.completed)
    }
  }
};
</script>

<style lang="stylus" scoped>
.real-app {
  width: 600px;
  margin: 0 auto;
  box-shadow: 0 0 5px #666;
}

.add-input {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  outline: none;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  font-smoothing: antialiased;
  padding: 16px 16px 16px 60px;
  border: none;
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}
</style>


