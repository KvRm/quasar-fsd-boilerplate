<template>
  <div>
    <p>{{ title }}</p>
    <ul>
      <li
        v-for="todo in todos"
        :key="todo.id"
        @click="increment"
        @keypress.enter="increment"
        role="button"
        tabIndex="0"
      >
        {{ todo.id }} - {{ todo.content }}
      </li>
    </ul>
    <p>Count: {{ todoCount }} / {{ meta.totalCount }}</p>
    <p>Active: {{ active ? 'yes' : 'no' }}</p>
    <p>Clicks on todos: {{ clickCount }}</p>
    {{ counter }}
  </div>
</template>

<script setup lang="ts">
  import { computed, ref } from 'vue'
  import { Todo, Meta } from './models'
  import { useCounterStore } from 'src/entities/example-store'

  interface Props {
    title: string
    todos?: Todo[]
    meta: Meta
    active: boolean
  }
  const props = withDefaults(defineProps<Props>(), {
    todos: () => [],
  })

  const { counter } = useCounterStore()

  const clickCount = ref(0)
  function increment() {
    clickCount.value += 1
    return clickCount.value
  }

  const todoCount = computed(() => props.todos.length)
</script>
