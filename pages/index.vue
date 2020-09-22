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
            <editor-content
              class="prose lg:prose-xl"
              :editor="editor"
            ></editor-content>
          </div>
        </client-only>
      </div>
      <div>
        <div class="flex flex-col space-y-6">
          <div class="py-4 text-center">
            <h2 class="font-sans text-4xl font-bold text-green-500">Result</h2>
          </div>
          <div>
            <h3 class="font-sans text-3xl font-semibold text-green-500">
              HTML
            </h3>
            <div class="mt-4 break-words">{{ html }}</div>
          </div>
          <div>
            <h3 class="font-sans text-3xl font-semibold text-green-500">
              JSON
            </h3>
            <div class="mt-4 break-words">{{ json }}</div>
          </div>
          <div>
            <h3 class="font-sans text-3xl font-semibold text-green-500">
              Rendered HTML
            </h3>
            <!-- eslint-disable-next-line vue/no-v-html -->
            <div class="mt-4 prose break-words lg:prose-xl" v-html="html"></div>
          </div>
        </div>
      </div>
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
      content:
        '<h1>Irure&nbsp;exercitation&nbsp;est&nbsp;ut&nbsp;aute&nbsp;excepteur&nbsp;laboris.</h1><p>Excepteur&nbsp;aliqua&nbsp;amet&nbsp;pariatur&nbsp;commodo&nbsp;esse&nbsp;quis&nbsp;cupidatat&nbsp;quis&nbsp;adipisicing&nbsp;mollit.&nbsp;Aliqua&nbsp;sunt&nbsp;incididunt&nbsp;dolore&nbsp;proident&nbsp;adipisicing&nbsp;<strong>enim&nbsp;</strong>sit&nbsp;laborum.&nbsp;Dolore&nbsp;ex&nbsp;<em>reprehenderit&nbsp;</em>deserunt&nbsp;voluptate&nbsp;reprehenderit&nbsp;sint&nbsp;in&nbsp;excepteur.&nbsp;</p><blockquote><p>Deserunt&nbsp;nostrud&nbsp;tempor&nbsp;minim&nbsp;laboris&nbsp;cupidatat&nbsp;consequat&nbsp;minim&nbsp;non&nbsp;excepteur&nbsp;amet.&nbsp;</p></blockquote><p>Cupidatat&nbsp;est&nbsp;Lorem&nbsp;consequat&nbsp;qui&nbsp;occaecat&nbsp;duis&nbsp;sunt&nbsp;sint&nbsp;excepteur&nbsp;non&nbsp;ipsum&nbsp;tempor.&nbsp;</p><h2>Commodo&nbsp;ea&nbsp;amet&nbsp;reprehenderit&nbsp;irure&nbsp;sunt.</h2><p>Consequat&nbsp;quis&nbsp;ullamco&nbsp;cupidatat&nbsp;minim&nbsp;ea&nbsp;duis&nbsp;dolore&nbsp;qui&nbsp;anim.&nbsp;Duis&nbsp;elit&nbsp;eu&nbsp;exercitation&nbsp;elit&nbsp;sit&nbsp;ea&nbsp;sit&nbsp;esse&nbsp;laboris.</p>',
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

<style>
.ProseMirror {
  @apply p-4;
  @apply border;
}

.ProseMirror:focus {
  outline: none;
}
</style>
