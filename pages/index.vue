<template>
  <div class="max-w-5xl mx-auto p-4">
    <div class="py-4 text-center">
      <h1 class="text-5xl font-bold font-sans text-green-500">TipTap NuxtJS</h1>
    </div>
    <div class="flex flex-col mt-6 space-y-6">
      <div>
        <client-only>
          <editor-content :editor="editor"></editor-content>
        </client-only>
      </div>
      <div>{{ html }}</div>
      <div>{{ json }}</div>
    </div>
  </div>
</template>

<script>
import { Editor, EditorContent } from 'tiptap'

export default {
  components: {
    EditorContent
  },
  data() {
    return {
      editor: null,
      html: 'update content to see html',
      json: 'update content to see json'
    }
  },
  mounted() {
    this.editor = new Editor({
      content: '<p>a paragraph</p>',
      onUpdate: ({ getJSON, getHTML }) => {
        this.html = getHTML()
        this.json = getJSON()
      }
    })
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
