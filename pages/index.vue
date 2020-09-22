<template>
  <div class="max-w-5xl p-4 mx-auto">
    <div class="py-4 text-center">
      <h1 class="font-sans text-5xl font-bold text-green-500">TipTap NuxtJS</h1>
    </div>
    <div class="flex flex-col mt-6 space-y-6">
      <div>
        <client-only>
          <div class="space-y-4">
            <editor-menu-bar v-slot="{ commands, isActive }" :editor="editor">
              <div class="flex flex-wrap">
                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.bold() }"
                  @click="commands.bold"
                >
                  Bold
                </button>
                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.italic() }"
                  @click="commands.italic"
                >
                  Italic
                </button>
                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.strike() }"
                  @click="commands.strike"
                >
                  Strike
                </button>
                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.underline() }"
                  @click="commands.underline"
                >
                  Underline
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.code() }"
                  @click="commands.code"
                >
                  Code
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.paragraph() }"
                  @click="commands.paragraph"
                >
                  Paragraph
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.heading({ level: 1 }) }"
                  @click="commands.heading({ level: 1 })"
                >
                  H1
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.heading({ level: 2 }) }"
                  @click="commands.heading({ level: 2 })"
                >
                  H2
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.heading({ level: 3 }) }"
                  @click="commands.heading({ level: 3 })"
                >
                  H3
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.bullet_list() }"
                  @click="commands.bullet_list"
                >
                  UL
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.ordered_list() }"
                  @click="commands.ordered_list"
                >
                  OL
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.blockquote() }"
                  @click="commands.blockquote"
                >
                  Quote
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  :class="{ 'is-active': isActive.code_block() }"
                  @click="commands.code_block"
                >
                  Code
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  @click="commands.horizontal_rule"
                >
                  Hr
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  @click="commands.undo"
                >
                  Undo
                </button>

                <button
                  class="p-2 transition duration-500 rounded-md hover:bg-gray-200"
                  @click="commands.redo"
                >
                  Redo
                </button>
              </div>
            </editor-menu-bar>
            <editor-content :editor="editor"></editor-content>
          </div>
        </client-only>
      </div>
      <div>{{ html }}</div>
      <div>{{ json }}</div>
      <!-- eslint-disable-next-line vue/no-v-html -->
      <div v-html="html"></div>
    </div>
  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import {
  Blockquote,
  CodeBlock,
  HardBreak,
  Heading,
  HorizontalRule,
  OrderedList,
  BulletList,
  ListItem,
  TodoItem,
  TodoList,
  Bold,
  Code,
  Italic,
  Link,
  Strike,
  Underline,
  History
} from 'tiptap-extensions'

export default {
  components: {
    EditorContent,
    EditorMenuBar
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
      extensions: [
        new Blockquote(),
        new BulletList(),
        new CodeBlock(),
        new HardBreak(),
        new Heading({ levels: [1, 2, 3] }),
        new HorizontalRule(),
        new ListItem(),
        new OrderedList(),
        new TodoItem(),
        new TodoList(),
        new Link(),
        new Bold(),
        new Code(),
        new Italic(),
        new Strike(),
        new Underline(),
        new History()
      ],
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
