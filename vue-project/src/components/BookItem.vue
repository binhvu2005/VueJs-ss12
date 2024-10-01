<template>
    <div class="book-item">
      <div class="book-details">
        <p class="book-name">{{ book.name }}</p>
        <p class="book-dates">{{ book.borrowDate }} - {{ book.returnDate }}</p>
      </div>
      <div class="book-status">
        <label for="status">Trạng thái:</label>
        <select id="status" v-model="status" @change="updateStatus" :class="{ borrowed: status === 'borrowed', returned: status === 'returned' }">
          <option value="borrowed">Chưa trả</option>
          <option value="returned">Đã trả</option>
        </select>
      </div>
      <div class="book-actions">
        <button @click="editBook" class="edit-btn">Sửa</button>
        <button @click="deleteBook" class="delete-btn">Xóa</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const props = defineProps({
    book: Object
  });
  const emit = defineEmits(['edit', 'delete', 'statusChange']);
  
  const status = ref(props.book.status);
  
  const editBook = () => {
    emit('edit');
  };
  
  const deleteBook = () => {
    emit('delete');
  };
  
  const updateStatus = () => {
    emit('statusChange', status.value);
  };
  </script>
  
  <style scoped>
  .book-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border: 1px solid #ddd;
    border-radius: 8px;
    margin-bottom: 10px;
    background-color: #f9f9f9;
    transition: background-color 0.3s ease;
  }
  
  .book-item:hover {
    background-color: #f0f0f0;
  }
  
  .book-details {
    flex: 2;
  }
  
  .book-name {
    font-weight: bold;
    font-size: 16px;
  }
  
  .book-dates {
    color: #666;
    font-size: 14px;
    margin-top: 5px;
  }
  
  .book-status {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  
  #status {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%; /* Chiếm toàn bộ chiều rộng */
  }
  
  #status.borrowed {
    background-color: #d32f2f; /* Đỏ cho trạng thái "Chưa trả" */
    color: white; /* Màu chữ trắng */
  }
  
  #status.returned {
    background-color: #21f032; /* Xanh cho trạng thái "Đã trả" */
    color: white; /* Màu chữ trắng */
  }
  
  .book-actions {
    flex: 1;
    display: flex;
    justify-content: space-between;
    gap: 10px;
  }
  
  .edit-btn,
  .delete-btn {
    padding: 8px 12px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .edit-btn {
    background-color: #4CAF50;
    color: white;
  }
  
  .delete-btn {
    background-color: #f44336;
    color: white;
  }
  
  .edit-btn:hover {
    background-color: #45a049;
  }
  
  .delete-btn:hover {
    background-color: #d32f2f;
  }
  </style>
  