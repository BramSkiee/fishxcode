<script setup lang="ts">
import { ref, onMounted, onUnmounted, useTemplateRef } from 'vue'

interface TimelineItem {
  date: string
  title: string
  description?: string
  type?: 'feature' | 'fix' | 'breaking' | 'improvement'
}

defineProps<{ items: TimelineItem[] }>()

const container = useTemplateRef<HTMLElement>('containerRef')
const visibleSet = ref(new Set<number>())
let observer: IntersectionObserver | null = null

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((e) => {
        const idx = Number((e.target as HTMLElement).dataset.idx)
        if (e.isIntersecting) visibleSet.value.add(idx)
      })
    },
    { threshold: 0.15 }
  )
  container.value?.querySelectorAll('[data-idx]').forEach((el) => observer!.observe(el))
})

onUnmounted(() => observer?.disconnect())

const TYPE_LABELS: Record<string, string> = {
  feature: '新功能',
  fix: '修复',
  breaking: '破坏性变更',
  improvement: '优化',
}
</script>

<template>
  <div ref="containerRef" class="timeline">
    <div
      v-for="(item, i) in items" :key="i"
      class="timeline-item"
      :class="[item.type ?? 'feature', { visible: visibleSet.has(i) }]"
      :data-idx="i"
    >
      <div class="dot" />
      <div class="content">
        <span class="date">{{ item.date }}</span>
        <span v-if="item.type" class="type-badge" :class="item.type">
          {{ TYPE_LABELS[item.type] ?? item.type }}
        </span>
        <h4 class="item-title">{{ item.title }}</h4>
        <p v-if="item.description" class="item-desc">{{ item.description }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.timeline {
  position: relative;
  padding-left: 28px;
  margin: 1.5rem 0;
}

/* 竖线 */
.timeline::before {
  content: '';
  position: absolute;
  left: 7px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: var(--vp-c-divider);
}

.timeline-item {
  position: relative;
  padding: 0 0 2rem 24px;
  opacity: 0;
  transform: translateY(16px);
  transition: opacity 0.45s ease, transform 0.45s ease;
}

.timeline-item.visible {
  opacity: 1;
  transform: translateY(0);
}

/* 圆点 */
.dot {
  position: absolute;
  left: -24px;
  top: 4px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  border: 2px solid var(--vp-c-bg);
  box-shadow: 0 0 0 2px var(--vp-c-divider);
  background: var(--vp-c-brand-1);
}

.timeline-item.fix .dot       { background: var(--vp-c-green-1); box-shadow: 0 0 0 2px var(--vp-c-green-1); }
.timeline-item.breaking .dot  { background: var(--vp-c-red-1);   box-shadow: 0 0 0 2px var(--vp-c-red-1); }
.timeline-item.improvement .dot { background: var(--vp-c-indigo-1); box-shadow: 0 0 0 2px var(--vp-c-indigo-1); }
.timeline-item.feature .dot   { background: var(--vp-c-brand-1); box-shadow: 0 0 0 2px var(--vp-c-brand-1); }

/* 内容 */
.content {
  padding: 0;
}

.date {
  font-size: 0.8rem;
  color: var(--vp-c-text-3);
  margin-right: 8px;
}

.type-badge {
  display: inline-block;
  font-size: 0.7rem;
  font-weight: 600;
  padding: 1px 8px;
  border-radius: 10px;
  vertical-align: middle;
}

.type-badge.feature     { background: var(--vp-c-brand-soft); color: var(--vp-c-brand-1); }
.type-badge.fix         { background: var(--vp-c-green-soft, rgba(16,185,129,.14)); color: var(--vp-c-green-1); }
.type-badge.breaking    { background: var(--vp-c-red-soft, rgba(244,63,94,.14));   color: var(--vp-c-red-1); }
.type-badge.improvement { background: var(--vp-c-indigo-soft); color: var(--vp-c-indigo-1); }

.item-title {
  font-size: 1rem;
  font-weight: 600;
  color: var(--vp-c-text-1);
  margin: 6px 0 4px;
}

.item-desc {
  font-size: 0.9rem;
  color: var(--vp-c-text-2);
  margin: 0;
  line-height: 1.6;
}

/* 响应式 */
@media (max-width: 480px) {
  .timeline { padding-left: 22px; }
  .timeline-item { padding-left: 18px; }
  .dot { left: -19px; width: 14px; height: 14px; }
}
</style>
