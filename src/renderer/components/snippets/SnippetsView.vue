<template>
  <div class="snippets-view">
    <SnippetHeader />
    <TheEditor
      v-model="snippet"
      v-model:lang="lang"
      :fragments="snippetStore.isFragmentsShow"
    />
  </div>
</template>

<script setup lang="ts">
import { useSnippetStore } from '@/store/snippets'
import { computed } from 'vue'

const snippetStore = useSnippetStore()

const snippet = computed({
  get: () => snippetStore.currentContent || '',
  set: v => {
    if (!v) return
    if (snippetStore.currentContent !== v) {
      snippetStore.patchCurrentSnippetContentByKey('value', v)
    }
  }
})

const lang = computed({
  get: () => snippetStore.currentLanguage || 'plain_text',
  set: v => {
    snippetStore.patchCurrentSnippetContentByKey('language', v)
  }
})
</script>

<style lang="scss" scoped>
.snippets-view {
  padding-top: var(--title-bar-height);
}
</style>