<template>
  <div class="test-form">
    <h2 class="test-form-title">Тестирование</h2>
    <p v-if="currentWord" class="current-word">{{ currentWord.word }}</p>
    <input type="text" v-model="userTranslation" placeholder="Перевод" class="translation-input">
    <button @click="checkTranslation" class="check-button" :disabled="userTranslation === ''">Проверить</button>
    <p v-if="showResult" class="result">{{ result }}</p>
  </div>
</template>
  
<script>
export default {
  props: ['words'],
  data() {
    return {
      currentWordIndex: null,
      userTranslation: '',
      showResult: false,
      result: ''
    }
  },
  computed: {
    currentWord() {
      if (this.currentWordIndex !== null) {
        return this.words[this.currentWordIndex];
      }
      return null;
    }
  },
  methods: {
    startTest() {
      this.currentWordIndex = Math.floor(Math.random() * this.words.length);
    },
    checkTranslation() {
      if (this.userTranslation.toLowerCase() === this.currentWord.translation.toLowerCase()) {
        this.result = 'Правильно!';
      } else {
        this.result = 'Неправильно!';
      }
      this.showResult = true;
      this.startTest();
      setTimeout(() => {
        this.showResult = false;
      }, 1000);
      setTimeout(() => {
        this.userTranslation = '';
      }, 1000);
    }
  },
  mounted() {
    this.startTest();
  }
}
</script>

<style>
.test-form {
  margin-top: 20px;
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.test-form-title {
  margin-bottom: 10px;
  color: #333;
  font-size: 20px;
}

.current-word {
  margin-bottom: 10px;
  font-size: 18px;
}

.translation-input {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.check-button {
  background-color: #3498db;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
}

.check-button:hover {
  background-color: #2980b9;
}

.result {
  margin-top: 10px;
  font-size: 18px;
}

</style>