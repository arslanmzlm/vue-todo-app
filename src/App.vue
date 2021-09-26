<template>
  <div id="app">
    <AppHeader :theme="theme" @toggle-theme="changeTheme()" />
    <AddTodo @add-todo="addTodo" />
    <div class="todos" v-if="getTodos.length">
      <TodoItem
        v-for="(todo, index) in getTodos"
        :key="index"
        :id="todo.id"
        :title="todo.title"
        :completed="todo.completed"
        @toggle-complete="toggleTodo"
        @remove-todo="removeTodo"
      />
      <TodoFooter
        :active="activeCount"
        :type="type"
        @change-type="changeType"
        @clear-completed="clearCompleted"
      />
    </div>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AddTodo from "./components/AddTodo.vue";
import TodoItem from "./components/TodoItem.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  name: "App",
  components: { AppHeader, AddTodo, TodoItem, TodoFooter },
  data() {
    return {
      theme: "dark",
      type: "all",
      todos: [
        { id: 1, title: "Lorem ipsum dolor sit amet.", completed: true },
        { id: 2, title: "Consectetur adipisicing elit.", completed: false },
        { id: 3, title: "Iure inventore rem, explicabo sint quisquam.", completed: false },
        { id: 4, title: "Adipisci odio quis dolores, tempora.", completed: false },
        { id: 5, title: "Bore amet nobis temporibus ius.", completed: false },
        { id: 6, title: "Reiciendis qui quia atque fugiat.", completed: false },
      ],
    };
  },
  methods: {
    changeTheme: function() {
      this.theme = this.theme == "dark" ? "light" : "dark";
      document.body.classList.remove("dark");
      document.body.classList.remove("light");
      document.body.classList.add(this.theme);
    },
    addTodo: function(todo) {
      this.todos.push({
        id: this.lastId + 1,
        title: todo,
        completed: false,
      });
    },
    findTodoKey: function(id) {
      let index;
      this.todos.forEach((todo, key) => {
        if (todo.id == id) {
          index = key;
        }
      });
      return index;
    },
    toggleTodo: function(id) {
      let index = this.findTodoKey(id);
      this.todos[index].completed = !this.todos[index].completed;
    },
    removeTodo: function(id) {
      let index = this.findTodoKey(id);
      this.todos.splice(index, 1);
    },
    clearCompleted: function() {
      let activeTodos = [];
      this.todos.forEach((todo) => {
        if (todo.completed !== true) {
          activeTodos.push(todo);
        }
      });
      this.todos = activeTodos;
      this.changeType("all");
    },
    changeType: function(type) {
      this.type = type;
    },
  },
  computed: {
    todoId: function() {
      return this.todos.length;
    },
    lastId: function() {
      let max = 0;
      this.todos.forEach((todo) => {
        max = todo.id > max ? todo.id : max;
      });
      return max;
    },
    activeCount: function() {
      let active = this.todos.length;
      this.todos.forEach((todo) => {
        if (todo.completed === true) {
          active--;
        }
      });
      return active;
    },
    completedCount: function() {
      let active = 0;
      this.todos.forEach((todo) => {
        if (todo.completed === true) {
          active++;
        }
      });
      return active;
    },
    getTodos: function() {
      let todos = [];
      if (this.type == "active" && this.activeCount > 0) {
        this.todos.forEach((todo) => {
          if (todo.completed !== true) {
            todos.push(todo);
          }
        });
      } else if (this.type == "completed" && this.completedCount > 0) {
        this.todos.forEach((todo) => {
          if (todo.completed === true) {
            todos.push(todo);
          }
        });
      } else {
        todos = this.todos;
        this.changeType("all");
      }
      return todos;
    },
  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap-reboot";

body {
  background-color: hsl(235, 21%, 11%);
  background-image: url("./assets/images/bg-desktop-dark.jpg");
  background-repeat: no-repeat;
  background-size: 100%;
  color: #fff;
}

body.light {
  background-color: hsl(0, 0%, 98%);
  background-image: url("./assets/images/bg-desktop-light.jpg");
}

#app {
  margin: 80px auto 0;
  max-width: 540px;
  font-family: "Josefin Sans", sans-serif;
  font-size: 18px;
}

@media screen and (max-width: 992px) {
  #app {
    width: 420px;
  }
}

@media screen and (max-width: 540px) {
  body {
    background-image: url("./assets/images/bg-mobile-dark.jpg");
  }

  body.light {
    background-image: url("./assets/images/bg-mobile-light.jpg");
  }

  #app {
    margin-top: 35px;
    width: 320px;
  }

  .header {
    margin-bottom: 25px;
  }
}

.todos {
  border-radius: 5px;
  box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);

  > div {
    background-color: hsl(235, 24%, 19%);
  }

  > div:first-child {
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }

  > div:not(:last-child) {
    border-bottom: 1px solid hsl(235, 17%, 26%);
  }
}

.light {
  .add-todo .input-add input {
    background-color: hsl(0, 0%, 100%);
    color: hsl(237, 12%, 35%);

    &::placeholder {
      color: hsl(240, 3%, 87%);
    }
  }

  .todos {
    > div {
      background-color: hsl(0, 0%, 100%);
    }

    > div:not(:last-child) {
      border-color: hsl(252, 10%, 90%);
    }

    .todo-item {
      color: hsl(237, 12%, 35%);

      &.active {
        color: hsl(240, 3%, 87%);
      }

      &:not(.active) .todo-circle:hover::before {
        background-color: hsl(0, 0%, 100%);
      }
    }
  }

  .todo-footer {
    color: hsl(250, 3%, 53%);

    & > div {
      background-color: hsl(0, 0%, 100%);
    }
  }
}
</style>
