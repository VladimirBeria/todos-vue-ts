<template>
  <li
    :class="{'todo-item--done': todo.completed}"
    class="todo-item"
    @click="toggleTodo"
  >
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import {Todo} from "@/types/Todo";

export default defineComponent({
  name: "AppTodoListItem",
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true,
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  },
  methods: {
    toggleTodo() {
      this.$emit('toggleTodo', this.todo.id)
    },
    removeTodo() {
      this.$emit('removeTodo', this.todo.id)
    }
  }
})
</script>


<style scoped>

</style>
