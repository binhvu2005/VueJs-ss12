<template>
  <div class="book-list">
    <BookItem 
      v-for="book in books" 
      :key="book.id" 
      :book="book" 
      @edit="openEditForm(book)" 
      @delete="deleteBook(book)" 
      @statusChange="updateStatus"
    />
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import BookItem from './BookItem.vue';

const props = defineProps({
  books: Array
});

const emit = defineEmits(['edit', 'delete', 'statusChange']);

const openEditForm = (book) => {
  emit('edit', book);
};

const deleteBook = (book) => {
  emit('delete', book);
};

const updateStatus = (status) => {
  emit('statusChange', status);
};
</script>
  </script>
  
  <style scoped>
  .book-list {
    margin-top: 20px;
    width: 100%;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }
  
  th, td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }
  
  th {
    background-color: #f2f2f2;
  }
  
  .edit-btn {
    background-color: #4CAF50;
    color: white;
    border: none;
    padding: 8px 12px;
    cursor: pointer;
  }
  
  .delete-btn {
    background-color: #f44336;
    color: white;
    border: none;
    padding: 8px 12px;
    cursor: pointer;
  }
  
  .edit-btn:hover, .delete-btn:hover {
    opacity: 0.8;
  }
  
  select {
    padding: 5px;
    font-size: 14px;
  }
  </style>
  