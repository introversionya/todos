<template>
  <section class="add-todo">
    <form @submit.prevent="addTodo" v-if="isFormVisible" class="add-todo__form">
      <button
        class="close-button"
        type="button"
        @click="closeForm"
      >
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showFrom">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { Todo } from '@/types/Todo'

interface State {
  isFormVisible: boolean,
  todoText: string
}

export default defineComponent({
  data(): State {
    return {
      isFormVisible: false,
      todoText: ''
    }
  },
  methods: {
    showFrom() {
      this.isFormVisible = true
    },
    closeForm() {
      this.isFormVisible = false
    },
    addTodo() {
      this.$emit('addTodo', {
        id: Date.now(),
        text: this.todoText,
        completed: false
      })

      this.todoText = ''
    }
  },
  emits: {
    addTodo: (todo: Todo) => todo
  }
})
</script>
