<template>
  <app-header />
  <app-filters :active-filter="activeFilter" @set-filter="setFilter" />
  <main class="app-main">
    <app-todo-list :todos="filteredTodos" @toggle-todo="toggleTodo" @remove-todo="removeTodo" />
    <app-add-todo @add-todo="addTodo" />
  </main>
  <app-footer :stats="stats" />
</template>
<script lang="ts">
import AppHeader from "@/components/AppHeader.vue";
import {defineComponent} from "vue";
import AppFilters from "@/components/AppFilters.vue";
import AppFooter from "@/components/AppFooter.vue";
import AppTodoList from "@/components/AppTodoList.vue";
import AppAddTodo from "@/components/AppAddTodo.vue";
import {Todo} from "@/types/Todo";
import {Filters} from "@/types/Filters";
import {Stats} from "@/types/Stats";

interface State {
  todos: Todo[],
  activeFilter: Filters,
}

export default defineComponent({
  name: "App",
  components: {
    AppAddTodo,
    AppTodoList,
    AppFooter,
    AppFilters,
    AppHeader,
  },

  data(): State {
    return {
      todos: [
        {id: 0, text: 'Learn the basics of Vue', completed: true},
        {id: 1, text: 'Learn the basics of Typescript', completed: false},
        {id: 2, text: 'Subscribe to the channel', completed: false},
      ],
      activeFilter: 'All',
    }
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos
        case 'Done':
          return this.doneTodos
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length,
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => !todo.completed)
    },
    doneTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => todo.completed)
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo)
    },
    toggleTodo(id: number) {
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeTodo(id: number) {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    },
    setFilter(filter: Filters) {
      this.activeFilter = filter
    }
  }
})
</script>
<style>
</style>
