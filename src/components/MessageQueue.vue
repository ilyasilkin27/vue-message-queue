<template>
  <div v-if="currentMessage" class="queue-block d-flex align-items-center mb-2">
    <button class="queue-x-btn me-3" @click="remove(currentMessage.id)">
      <span aria-label="Удалить" class="queue-x">✕</span>
    </button>
    <span class="queue-text">{{ currentMessage.text }}</span>
  </div>
</template>

<script setup lang="ts">
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
const props = defineProps<{
  messages: { id: number; text: string; createdAt: Date; removed: boolean }[]
}>()
const emit = defineEmits(['remove'])

const currentMessage = ref<{
  id: number
  text: string
  createdAt: Date
  removed: boolean
} | null>(null)
let timer: ReturnType<typeof setTimeout> | null = null

const showNext = () => {
  const next = props.messages.find(
    (m) => !m.removed && m !== currentMessage.value
  )
  currentMessage.value = next || null
  if (timer) clearTimeout(timer)
  if (next) {
    timer = setTimeout(showNext, 3000)
  }
}

watch(() => props.messages.map((m) => m.removed), showNext, { immediate: true })
onMounted(showNext)
onBeforeUnmount(() => {
  if (timer) clearTimeout(timer)
})

const remove = (id: number) => {
  emit('remove', id)
  showNext()
}
</script>

<style scoped>
.queue-block {
  background: #d6f5e3;
  border-radius: 16px 16px 0 0;
  padding: 32px 48px;
  min-height: 72px;
  font-size: 22px;
  font-weight: 500;
  margin-bottom: 0;
  width: 100%;
  box-sizing: border-box;
}
@media (max-width: 900px) {
  .queue-block {
    padding: 20px 20px;
    font-size: 18px;
    min-height: 48px;
  }
}
@media (max-width: 600px) {
  .queue-block {
    padding: 12px 8px;
    font-size: 15px;
    border-radius: 10px 10px 0 0;
    min-height: 36px;
  }
  .queue-x {
    font-size: 18px;
  }
}
.queue-x-btn {
  background: none;
  border: none;
  outline: none;
  padding: 0;
  margin-right: 18px;
  cursor: pointer;
  display: flex;
  align-items: center;
}
.queue-x {
  font-size: 28px;
  color: #3a5743;
  line-height: 1;
}
.queue-text {
  flex: 1;
}
</style>
