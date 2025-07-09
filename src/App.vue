<template>
  <div class="app-bg">
    <div class="main-card">
      <MessageQueue :messages="messages" @remove="removeMessage" />
      <MessageList :messages="messages" @remove="removeMessage" />
      <MessageInput @add="addMessage" />
    </div>
  </div>
</template>

<script setup lang="ts">
import MessageQueue from './components/MessageQueue.vue'
import MessageList from './components/MessageList.vue'
import MessageInput from './components/MessageInput.vue'
import { ref } from 'vue'

const messages = ref<
  {
    id: number
    text: string
    createdAt: Date
    removed: boolean
  }[]
>([])

const addMessage = (text: string) => {
  messages.value.push({
    id: Date.now() + Math.random(),
    text,
    createdAt: new Date(),
    removed: false,
  })
}

const removeMessage = (id: number) => {
  const msg = messages.value.find((m) => m.id === id)
  if (msg) msg.removed = true
}
</script>

<style scoped>
.app-bg {
  min-height: 100dvh;
  min-width: 100vw;
  background: #f7f8fa;
  display: flex;
  align-items: stretch;
  justify-content: stretch;
}
.main-card {
  background: #fff;
  border-radius: 0;
  box-shadow: none;
  padding: 64px 0 0 0;
  width: 100vw;
  height: 100dvh;
  min-height: 100dvh;
  max-width: 100vw;
  max-height: 100dvh;
  display: flex;
  flex-direction: column;
  gap: 36px;
  margin: 0;
  overflow: hidden;
}
@media (max-width: 900px) {
  .main-card {
    padding: 24px 0 0 0;
    gap: 16px;
  }
}
@media (max-width: 600px) {
  .main-card {
    padding: 8px 0 0 0;
    gap: 8px;
  }
}
</style>
