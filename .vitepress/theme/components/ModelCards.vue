<script setup lang="ts">
interface Model {
  name: string
  description: string
  tags?: string[]
}

defineProps<{ models: Model[] }>()

const tagColors: Record<string, { bg: string; color: string }> = {
  '推荐': { bg: 'var(--vp-c-brand-soft)', color: 'var(--vp-c-brand-1)' },
  '快速': { bg: 'var(--vp-c-tip-soft)', color: 'var(--vp-c-tip-1)' },
  '强力': { bg: 'var(--vp-c-warning-soft)', color: 'var(--vp-c-warning-1)' },
}

const defaultTag = { bg: 'var(--vp-c-default-soft)', color: 'var(--vp-c-text-2)' }

function tagStyle(tag: string) {
  const c = tagColors[tag] || defaultTag
  return { backgroundColor: c.bg, color: c.color }
}
</script>

<template>
  <div class="model-grid">
    <div v-for="model in models" :key="model.name" class="model-card">
      <h3 class="name">{{ model.name }}</h3>
      <p class="desc">{{ model.description }}</p>
      <div v-if="model.tags?.length" class="tags">
        <span v-for="tag in model.tags" :key="tag" class="tag" :style="tagStyle(tag)">{{ tag }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.model-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
  margin: 16px 0;
}

@media (min-width: 640px) {
  .model-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 960px) {
  .model-grid { grid-template-columns: repeat(3, 1fr); }
}

.model-card {
  border: 1px solid var(--vp-c-divider);
  border-radius: 8px;
  padding: 20px;
  background: var(--vp-c-bg);
  transition: box-shadow 0.25s, transform 0.25s;
}

.model-card:hover {
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px);
}

.name {
  margin: 0 0 8px;
  font-size: 16px;
  font-weight: 600;
  color: var(--vp-c-text-1);
}

.desc {
  margin: 0 0 12px;
  font-size: 14px;
  color: var(--vp-c-text-2);
  line-height: 1.5;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.tag {
  display: inline-block;
  padding: 2px 8px;
  border-radius: 10px;
  font-size: 12px;
  font-weight: 500;
  line-height: 1.5;
}
</style>
