<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = withDefaults(defineProps<{
  text: string
  link?: string
  linkText?: string
  storageKey?: string
}>(), {
  storageKey: 'announcement-dismissed'
})

const visible = ref(false)

onMounted(() => {
  visible.value = !localStorage.getItem(props.storageKey)
})

function dismiss() {
  visible.value = false
  localStorage.setItem(props.storageKey, '1')
}
</script>

<template>
  <Transition name="slide-up">
    <div v-if="visible" class="announcement-bar">
      <div class="content">
        <span>{{ text }}</span>
        <a v-if="link" :href="link" class="link">{{ linkText || link }}</a>
      </div>
      <button class="close" aria-label="Close" @click="dismiss">&times;</button>
    </div>
  </Transition>
</template>

<style scoped>
.announcement-bar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 36px;
  background-color: var(--vp-c-brand-3);
  color: var(--vp-c-white);
  font-size: 14px;
}

.content {
  display: flex;
  align-items: center;
  gap: 8px;
}

.link {
  color: var(--vp-c-white);
  text-decoration: underline;
  font-weight: 500;
}

.close {
  position: absolute;
  right: 16px;
  background: none;
  border: none;
  color: var(--vp-c-white);
  font-size: 18px;
  cursor: pointer;
  line-height: 1;
  padding: 0 4px;
  opacity: 0.8;
  transition: opacity 0.2s;
}

.close:hover {
  opacity: 1;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.3s ease;
}

.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}
</style>
