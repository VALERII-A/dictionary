<template>
  <div class="import-form">
    <input type="file" @change="handleFile" class="file-input">
    <button @click="importWords" class="import-button" :disabled="!file">Импортировать</button>
  </div>
</template>

<script>
import Papa from 'papaparse';

export default {
  data() {
    return {
      file: null
    }
  },
  methods: {
    handleFile(event) {
      this.file = event.target.files[0];
    },
    importWords() {
      if (this.file) {
        const reader = new FileReader();
        reader.onload = () => {
          const csvData = reader.result;
          try {
            const parsedData = Papa.parse(csvData, { header: true }).data;
            this.$emit('import-words', parsedData);
          } catch (error) {
            console.error('Ошибка при импорте данных:', error);
          }
        }
        reader.onerror = (error) => {
          console.error('Ошибка при чтении файла:', error);
        }
        reader.readAsText(this.file);
      }
    }
  }
}
</script>

<style>
.import-form {
  margin-top: 20px;
}

.file-input {
  margin-right: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.import-button {
  background-color: #27ae60;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 3px;
  cursor: pointer;
}

.import-button:hover {
  background-color: #219653;
}

</style>