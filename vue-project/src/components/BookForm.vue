<template>
    <div class="form-container">
      <form @submit.prevent="saveBook">
        <div class="form-group">
          <label for="name">Tên sách:</label>
          <input id="name" v-model="book.name" required />
        </div>
        <div class="form-group">
          <label for="borrower">Tên người mượn:</label>
          <input id="borrower" v-model="book.borrower" required />
        </div>
        <div class="form-group">
          <label for="borrowDate">Ngày mượn:</label>
          <input id="borrowDate" type="date" v-model="book.borrowDate" required />
        </div>
        <div class="form-group">
          <label for="returnDate">Ngày trả:</label>
          <input id="returnDate" type="date" v-model="book.returnDate" required />
        </div>
        <div class="form-actions">
          <button type="submit" class="save-btn">Lưu</button>
          <button type="button" @click="$emit('close')" class="cancel-btn">Hủy</button>
        </div>
      </form>
    </div>
  </template>
  
  <script setup>
  import { reactive, watchEffect } from 'vue';
  
  const props = defineProps({
    book: Object
  });
  
  const emit = defineEmits(['save', 'close']);
  
  const book = reactive({
    name: '',
    borrower: '',
    borrowDate: '',
    returnDate: '',
    status: 'borrowed'
  });
  
  watchEffect(() => {
    if (props.book) {
      Object.assign(book, props.book); 
    }
  });
  
  const saveBook = () => {
    if (book.borrowDate <= book.returnDate) {
      emit('save', { ...book });
    } else {
      alert('Ngày mượn không thể lớn hơn ngày trả!');
    }
  };
  </script>
  
  <style scoped>
  .form-container {
    position: fixed;
    top: 200px;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000; 
    max-width: 400px;
    max-height: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  .form-group label {
    display: block;
    margin-bottom: 5px;
    font-weight: bold;
  }
  
  .form-group input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .form-actions {
    display: flex;
    justify-content: space-between;
  }
  
  .save-btn {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .cancel-btn {
    background-color: #f44336;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .save-btn:hover, .cancel-btn:hover {
    opacity: 0.8;
  }
  </style>
  