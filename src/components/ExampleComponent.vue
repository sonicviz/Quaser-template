<script setup lang="ts">
import type { Meta, Todo } from './models'

interface Props {
  title: string
  todos?: Todo[]
  meta: Meta
  active: boolean
}
const props = withDefaults(defineProps<Props>(), {
  todos: () => [],
})

const clickCount = ref(0)
function increment() {
  clickCount.value += 1
  return clickCount.value
}

const todoCount = computed(() => props.todos.length)
</script>

<template>
  <div>
    <p>{{ title }}</p>
    <ul>
      <li
        v-for="todo in todos"
        :key="todo.id"
        @click="increment"
      >
        {{ todo.id }} - {{ todo.content }}
      </li>
    </ul>
    <p>Count: {{ todoCount }} / {{ meta.totalCount }}</p>
    <p class="mt-8">
      Active: {{ active ? 'yes' : 'no' }}
    </p>
    <p>Clicks on todos: {{ clickCount }}</p>
    <button
      bg="red-500 hover:red-600 dark:blue-500 dark:hover:red-600"
      text="sm white"
      p="y-2 x-4"
      border="2 rounded red-600"
      mt="2"
    >
      Button
    </button>
  </div>
</template>
