<template>
    <div class="app-container">
      <h1>Quản lý mượn trả sách</h1>
      <button @click="openAddForm" class="add-button">Thêm thông tin</button>
  
      <BookForm v-if="isFormVisible" @save="handleSave" @close="closeForm" :editData="currentEditData" />
  
      <BookList 
        :books="books" 
        @delete="openDeleteModal" 
        @edit="openEditForm"
        @statusChange="handleStatusChange" 
      />
  
      <Modal v-if="isDeleteModalVisible" @confirm="confirmDelete" @cancel="closeDeleteModal" />
    </div>
  </template>
  
  <script setup>
  import { ref, reactive } from 'vue'
  import BookList from './components/BookList.vue'
  import BookForm from './components/BookForm.vue'
  import Modal from './components/Modal.vue'
  
  const books = ref(JSON.parse(localStorage.getItem('books')) || [])
  const isFormVisible = ref(false)
  const isDeleteModalVisible = ref(false)
  const currentEditData = ref(null)
  const bookToDelete = ref(null)
  
  const openAddForm = () => {
    currentEditData.value = null
    isFormVisible.value = true
  }
  
  const openEditForm = (book) => {
    currentEditData.value = book
    isFormVisible.value = true
  }
  
  const handleSave = (book) => {
    if (currentEditData.value) {
      const index = books.value.findIndex(item => item.id === book.id)
      books.value.splice(index, 1, book)
    } else {
      book.id = Date.now()
      books.value.push(book)
    }
    localStorage.setItem('books', JSON.stringify(books.value))
    isFormVisible.value = false
  }
  
  const handleStatusChange = (bookId, status) => {
    const book = books.value.find(item => item.id === bookId)
    if (book) {
      book.status = status
      localStorage.setItem('books', JSON.stringify(books.value))
    }
  }
  
  const openDeleteModal = (book) => {
    bookToDelete.value = book
    isDeleteModalVisible.value = true
  }
  
  const confirmDelete = () => {
    books.value = books.value.filter(book => book.id !== bookToDelete.value.id)
    localStorage.setItem('books', JSON.stringify(books.value))
    closeDeleteModal()
  }
  
  const closeDeleteModal = () => {
    isDeleteModalVisible.value = false
  }
  
  const closeForm = () => {
    isFormVisible.value = false
  }
  </script>
  
  <style scoped>
  .app-container {
    padding: 20px;
    background-color: #f9f9f9; 
    border-radius: 8px; 
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    max-width: 800px; 
    margin: auto; 
  }
  
  h1 {
    text-align: center; 
    color: #333; 
    margin-bottom: 20px; 
  }
  
  .add-button {
    display: block;
    width: 100%; 
    padding: 10px;
    background-color: #4CAF50; 
    color: white;
    border: none; 
    border-radius: 5px; 
    font-size: 16px;
    cursor: pointer; 
    transition: background-color 0.3s; 
  }
  
  .add-button:hover {
    background-color: #45a049; 
  }
  
  button {
    margin-bottom: 20px; 
  }
  </style>
  