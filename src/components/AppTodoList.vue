<template>
  <ul class="todo-list">
    <app-todo-list-item
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import AppTodoListItem from "@/components/AppTodoListItem.vue";
import {Todo} from "@/types/Todo";


export default defineComponent({
  name: "AppTodoList",
  components: {AppTodoListItem},
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
      required: true,
    }
  },
  methods: {
    toggleTodo(id: number) {
      this.$emit('toggleTodo', id)
    },
    removeTodo(id: number) {
      this.$emit('removeTodo', id)
    }
  },
})
</script>


<style scoped>

</style>
