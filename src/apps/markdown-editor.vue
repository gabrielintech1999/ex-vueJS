<template>
    <div>
      <h1>Markdown Editor</h1>
      <div class="editor">
        <textarea v-model="markdownText" placeholder="Write Markdown here..."></textarea>
      </div>
      <div class="preview" v-html="renderedMarkdown"></div>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue';
  import {marked} from 'marked';
  
  export default {
    setup() {
      const markdownText = ref('');
  
      // Converte o markdown para HTML usando a biblioteca "marked"
      const renderedMarkdown = computed(() => {
        return marked(markdownText.value);
      });
  
      return {
        markdownText,
        renderedMarkdown,
      };
    },
  };
  </script>
  
  <style>
  .editor, .preview {
    width: 100%;
    padding: 10px;
    box-sizing: border-box;
  }
  textarea {
    width: 100%;
    height: 200px;
  }
  .preview {
    margin-top: 20px;
    border: 1px solid #ddd;
    padding: 10px;
  }
  </style>
  