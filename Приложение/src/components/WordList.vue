<template>
  <div class="word-list">
    <ul>
      <li v-for="word in words" :key="word.word" class="word-item">
        {{ word.word }} - {{ word.translation }}
        <button @click="removeWord(word)" class="remove-button">Удалить</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['words'],
  methods: {
    removeWord(word) {
      this.$emit('remove-word', word);
    }
  }
}
</script>

<style>
.word-list {
  margin-top: 20px;
}

.word-item {
  margin-bottom: 10px;
  background-color: #fff;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.remove-button {
  background-color: #e74c3c;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 3px;
  cursor: pointer;
}

.remove-button:hover {
  background-color: #c0392b;
}

</style>