<template>
  <div class="modal-overlay" @click="cancelDelete">
    <div class="modal-content" @click.stop>
      <p>Bạn có chắc chắn muốn xóa thông tin này?</p>
      <div class="modal-actions">
        <button @click="confirmDelete" class="confirm-btn">Xóa</button>
        <button @click="cancelDelete" class="cancel-btn">Hủy</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['confirm', 'cancel'])

const confirmDelete = () => {
  emit('confirm')
}

const cancelDelete = () => {
  emit('cancel')
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5); 
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000; 
}

.modal-content {
  background-color: white; 
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2); 
  text-align: center; 
}

.modal-actions {
  display: flex;
  justify-content: space-around; 
  margin-top: 20px; 
}

.confirm-btn, .cancel-btn {
  padding: 10px 15px; 
  border-radius: 4px; 
  cursor: pointer; 
}

.confirm-btn {
  background-color: #f44336;
  color: white;
}

.cancel-btn {
  background-color: #4CAF50;
  color: white;
}

.confirm-btn:hover, .cancel-btn:hover {
  opacity: 0.8; 
}
</style>
