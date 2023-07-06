<template>
  <div class="add-word-form">
    <input type="text" v-model="word" placeholder="Слово" class="word-input">
    <input type="text" v-model="translation" placeholder="Перевод" class="translation-input">
    <button @click="addWord" class="add-button">Добавить</button>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      word: '',
      translation: ''
    }
  },
  methods: {
    addWord() {
      if (this.word !== '' && this.translation !== '') {
        const newWord = {
          word: this.word,
          translation: this.translation
        }
        this.$emit('add-word', newWord);
        this.word = '';
        this.translation = '';
      }
    }
  }
}
</script>

<style>
.add-word-form {
  margin-top: 20px;
}

.word-input {
  margin-right: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.translation-input {
  margin-right: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.add-button {
  background-color: #e67e22;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
}

.add-button:hover {
  background-color: #d35400;
}

</style>
  