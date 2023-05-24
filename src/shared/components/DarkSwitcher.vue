<template>
  <q-toggle
    v-model="isDarkTheme"
    color="blue-grey-10"
    checked-icon="dark_mode"
    unchecked-icon="light_mode"
    icon-color="blue-grey-2"
  />
</template>

<script setup lang="ts">
  import { useQuasar } from 'quasar'
  import { ref, watch } from 'vue'

  const $q = useQuasar()

  const isDarkTheme = ref<boolean>($q.dark.isActive)

  watch(isDarkTheme, (value) => {
    $q.dark.set(value)
  })
</script>
