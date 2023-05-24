<template>
  <q-select
    v-model="currentLanguage"
    :options="langOptions"
    dense
    borderless
    emit-value
    map-options
    options-dense
    style="min-width: 150px"
  />
</template>

<script setup lang="ts">
  import { computed, ref, watch } from 'vue'
  import { useQuasar } from 'quasar'
  import { useI18n } from 'vue-i18n'
  import availableLangs from 'src/shared/i18n/index'

  const $q = useQuasar()

  const langOptions: { value: keyof typeof availableLangs; label: string }[] = [
    { value: 'en-US', label: 'English' },
    { value: 'ru', label: 'Русский' },
  ]

  const lang = ref($q.lang.isoName)
  const { locale } = useI18n({ useScope: 'global' })

  const currentLanguage = computed<string>({
    get() {
      return lang.value
    },
    set(value) {
      lang.value = value
      locale.value = value
    },
  })

  watch(lang, async (val) => {
    import(`../../../node_modules/quasar/lang/${val}.mjs`).then((lang) => {
      $q.lang.set(lang.default)
    })
  })
</script>
