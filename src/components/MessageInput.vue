<template>
  <form class="input-block d-flex align-items-center" @submit.prevent="submit">
    <input
      v-model="text"
      class="form-control input-custom flex-grow-1"
      type="text"
      placeholder="Новое сообщение"
      required
    />
    <button class="btn btn-success send-btn ms-2" type="submit">
      ОТПРАВИТЬ
    </button>
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const emit = defineEmits(['add'])
const text = ref('')

const submit = () => {
  if (text.value.trim()) {
    emit('add', text.value.trim())
    text.value = ''
  }
}
</script>

<style scoped>
.input-block {
  background: #fff;
  border-radius: 0 0 16px 16px;
  padding: 28px 48px 32px 48px;
  box-shadow: 0 -1px 8px 0 rgba(0, 0, 0, 0.03);
  margin-top: 0;
  width: 100%;
  box-sizing: border-box;
}
@media (max-width: 900px) {
  .input-block {
    padding: 16px 20px 18px 20px;
  }
}
@media (max-width: 600px) {
  .input-block {
    padding: 8px 8px 10px 8px;
    border-radius: 0 0 10px 10px;
  }
  .input-custom {
    font-size: 14px;
  }
  .send-btn {
    min-width: 80px;
    font-size: 14px;
    padding: 6px 0;
    border-radius: 6px;
  }
}
.input-custom {
  border: none;
  background: transparent;
  font-size: 20px;
  outline: none;
  box-shadow: none;
}
.send-btn {
  min-width: 160px;
  font-weight: 600;
  font-size: 20px;
  border-radius: 10px;
  box-shadow: none;
  padding: 12px 0;
}
</style>
