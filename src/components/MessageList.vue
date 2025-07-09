<template>
  <div class="list-block">
    <ul class="list-unstyled mb-0">
      <li
        v-for="msg in messages"
        :key="msg.id"
        class="d-flex align-items-center list-item"
        :class="{ 'text-muted': msg.removed }"
      >
        <span v-if="msg.removed" class="list-x me-2">✕</span>
        <span v-else class="list-x-placeholder me-2"></span>
        <span class="flex-grow-1">{{ msg.text }}</span>
        <span class="list-date ms-2">{{ formatDate(msg.createdAt) }}</span>
        <button
          v-if="!msg.removed"
          class="list-x-btn ms-2"
          @click="$emit('remove', msg.id)"
        >
          ✕
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  messages: { id: number; text: string; createdAt: Date; removed: boolean }[]
}>()
const formatDate = (date: Date) =>
  new Date(date).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })
</script>

<style scoped>
.list-block {
  background: #fff;
  border-radius: 0;
  box-shadow: 0 1px 8px 0 rgba(0, 0, 0, 0.03);
  padding: 32px 0 32px 0;
  min-height: 180px;
  max-height: 60vh;
  overflow-y: auto;
  margin-bottom: 0;
  width: 100%;
  box-sizing: border-box;
}
@media (max-width: 900px) {
  .list-block {
    padding: 16px 0 16px 0;
    max-height: 40vh;
  }
}
@media (max-width: 600px) {
  .list-block {
    padding: 8px 0 8px 0;
    max-height: 32vh;
  }
  .list-item {
    padding: 4px 12px 4px 10px;
    font-size: 14px;
    min-height: 28px;
  }
  .list-x,
  .list-x-btn,
  .list-x-placeholder {
    font-size: 15px;
    width: 15px;
  }
  .list-date {
    font-size: 10px;
    min-width: 32px;
  }
}
.list-item {
  padding: 12px 48px 12px 36px;
  font-size: 20px;
  border: none;
  background: none;
  min-height: 48px;
}
.list-x {
  color: #3a5743;
  font-size: 24px;
  width: 24px;
  display: inline-block;
  text-align: center;
}
.list-x-placeholder {
  width: 24px;
  display: inline-block;
}
.list-x-btn {
  background: none;
  border: none;
  color: #3a5743;
  font-size: 24px;
  cursor: pointer;
  padding: 0 2px;
  line-height: 1;
}
.list-date {
  font-size: 15px;
  color: #b0b0b0;
  min-width: 56px;
  text-align: right;
}
</style>
