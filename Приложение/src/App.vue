<template>
  <div class="app">
  
    <div class="left-side">
      <h1 class="app-title">Англо-русский словарь</h1>
      <add-word-form @add-word="addWord"></add-word-form>
      <word-list :words="words" @remove-word="removeWord"></word-list>
    </div>
    <div class="right-side">
      <test-form :words="words"></test-form>
      <import-form @import-words="importWords"></import-form>
    </div>
  </div>
</template>

<script>
import AddWordForm from './components/AddWordForm.vue';
import WordList from './components/WordList.vue';
import TestForm from './components/TestForm.vue';
import ImportForm from './components/ImportForm.vue';

export default {
  components: {
    AddWordForm,
    WordList,
    TestForm,
    ImportForm
  },
  data() {
    return {
      words: []
    }
  },
  methods: {
    addWord(word) {
      this.words.push(word);
    },
    removeWord(word) {
      const index = this.words.indexOf(word);
      if (index > -1) {
        this.words.splice(index, 1);
      }
    },
    importWords(words) {
      this.words = words;
    }
  }
}
</script>

<style>
.app {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  text-align: center;
  background-color: #f5f5f5;
  padding: 20px;
}

.app-title {
  margin-bottom: 20px;
  color: #333;
  font-size: 24px;
}

.left-side {
  width: 40%;
}

.right-side {
  width: 50%;
}

</style>