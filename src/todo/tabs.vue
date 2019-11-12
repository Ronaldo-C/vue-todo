<template>
  <div class="helper">
    <span class="left">{{todoItemsNum.length}} items left</span>
    <span class="tabs">
      <span
        v-for="(state, index) in states"
        :key="index"
        :class="[filter === state && 'actived']"
        @click="toggleFilter(state)"
      >{{ state }}</span>
    </span>
    <span class="clear" @click="clearCompleted">Clear Completed</span>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true
    },
    filter: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      states: ["all", "active", "completed"]
    };
  },
  computed: {
    todoItemsNum() {
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
    toggleFilter(state) {
      this.$emit('filterToggle', state)
    },
    clearCompleted() {
      this.$emit('clear')
    }
  }
};
</script>

<style lang="stylus" scoped>
.helper {
  font-weight: 100;
  display: flex;
  justify-content: space-between;
  padding: 5px 0;
  line-height: 30px;
  background-color: #fff;
  font-size: 14px;
  font-smoothing: antialiased;
}

.left, .clear, .tabs {
  padding: 0 10px;
  box-sizing: border-box;
}

.left, .clear {
  width: 150px;
}

.left {
  text-align: left;
}

.clear {
  text-align: right;
  cursor: pointer;
}

.tabs {
  width: 200px;
  display: flex;
  justify-content: space-around;

  * {
    display: inline-block;
    padding: 0 10px;
    cursor: pointer;
    border: 1px solid rgba(175, 47, 47, 0);

    &.actived {
      border-color: rgba(175, 47, 47, 0.4);
      border-radius: 5px;
    }
  }
}
</style>


