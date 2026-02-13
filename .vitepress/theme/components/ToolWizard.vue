<script setup lang="ts">
import { ref, computed } from 'vue'

const TEXT = {
  title: '找到最适合你的 AI Coding 工具',
  steps: ['使用场景', '偏好模型', '使用特点'],
  scenarioLabel: '你主要在哪里写代码？',
  scenarioOptions: ['CLI 终端', 'VS Code 编辑器', '两者都要'],
  modelLabel: '你偏好哪个 AI 模型？',
  modelOptions: ['Claude', 'GPT', 'Gemini', '不限'],
  traitLabel: '你最看重什么？',
  traitOptions: ['开箱即用', '高度可定制', '轻量快速'],
  resultPrefix: '推荐工具',
  viewGuide: '查看配置指南',
  restart: '重新选择',
} as const

const RECOMMENDATIONS: Record<string, { name: string; link: string }> = {
  'CLI 终端|Claude':   { name: 'Claude Code',   link: '/start' },
  'CLI 终端|GPT':      { name: 'OpenAI Codex',  link: '/codex' },
  'CLI 终端|Gemini':   { name: 'Gemini CLI',    link: '/gemini' },
  'VS Code 编辑器':    { name: 'RooCode',       link: '/roocode' },
  '轻量快速':          { name: 'Droid CLI',     link: '/droid' },
  '高度可定制':        { name: 'OpenCode',      link: '/opencode' },
}

const step = ref(0)
const scenario = ref('')
const model = ref('')
const trait = ref('')

const result = computed(() => {
  if (scenario.value === 'VS Code 编辑器')
    return RECOMMENDATIONS['VS Code 编辑器']
  if (trait.value === '轻量快速')
    return RECOMMENDATIONS['轻量快速']
  if (trait.value === '高度可定制')
    return RECOMMENDATIONS['高度可定制']
  const key = `${scenario.value}|${model.value}`
  return RECOMMENDATIONS[key] ?? { name: 'Claude Code', link: '/start' }
})

function selectScenario(val: string) {
  scenario.value = val
  if (val === 'VS Code 编辑器') { step.value = 3; return }
  step.value = 1
}

function selectModel(val: string) {
  model.value = val
  step.value = 2
}

function selectTrait(val: string) {
  trait.value = val
  step.value = 3
}

function restart() {
  step.value = 0
  scenario.value = ''
  model.value = ''
  trait.value = ''
}
</script>

<template>
  <div class="wizard">
    <h3 class="wizard-title">{{ TEXT.title }}</h3>

    <!-- 步骤指示器 -->
    <div class="steps-indicator">
      <template v-for="(label, i) in TEXT.steps" :key="i">
        <div class="step-dot" :class="{ active: step >= i, done: step > i }">
          <span class="dot">{{ step > i ? '&#10003;' : i + 1 }}</span>
          <span class="step-label">{{ label }}</span>
        </div>
        <div v-if="i < TEXT.steps.length - 1" class="step-line" :class="{ active: step > i }" />
      </template>
    </div>

    <!-- 选择区域 -->
    <Transition name="fade" mode="out-in">
      <!-- Step 1: 使用场景 -->
      <div v-if="step === 0" key="s0" class="options-panel">
        <p class="options-label">{{ TEXT.scenarioLabel }}</p>
        <div class="options-grid">
          <button
            v-for="opt in TEXT.scenarioOptions" :key="opt"
            class="option-card" :class="{ selected: scenario === opt }"
            @click="selectScenario(opt)"
          >{{ opt }}</button>
        </div>
      </div>

      <!-- Step 2: 偏好模型 -->
      <div v-else-if="step === 1" key="s1" class="options-panel">
        <p class="options-label">{{ TEXT.modelLabel }}</p>
        <div class="options-grid">
          <button
            v-for="opt in TEXT.modelOptions" :key="opt"
            class="option-card" :class="{ selected: model === opt }"
            @click="selectModel(opt)"
          >{{ opt }}</button>
        </div>
      </div>

      <!-- Step 3: 使用特点 -->
      <div v-else-if="step === 2" key="s2" class="options-panel">
        <p class="options-label">{{ TEXT.traitLabel }}</p>
        <div class="options-grid">
          <button
            v-for="opt in TEXT.traitOptions" :key="opt"
            class="option-card" :class="{ selected: trait === opt }"
            @click="selectTrait(opt)"
          >{{ opt }}</button>
        </div>
      </div>

      <!-- 结果 -->
      <div v-else key="result" class="result-panel">
        <p class="result-label">{{ TEXT.resultPrefix }}</p>
        <p class="result-name">{{ result.name }}</p>
        <div class="result-actions">
          <a class="btn-primary" :href="result.link">{{ TEXT.viewGuide }}</a>
          <button class="btn-secondary" @click="restart">{{ TEXT.restart }}</button>
        </div>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.wizard {
  max-width: 560px;
  margin: 2rem auto;
  padding: 2rem;
  border-radius: 12px;
  background: var(--vp-c-bg);
  border: 1px solid var(--vp-c-divider);
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.06);
}

.wizard-title {
  margin: 0 0 1.5rem;
  text-align: center;
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--vp-c-text-1);
}

/* 步骤指示器 */
.steps-indicator {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0;
  margin-bottom: 1.75rem;
}

.step-dot {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
}

.dot {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8rem;
  font-weight: 600;
  border: 2px solid var(--vp-c-divider);
  color: var(--vp-c-text-3);
  background: var(--vp-c-bg);
  transition: all 0.3s;
}

.step-dot.active .dot {
  border-color: var(--vp-c-brand-1);
  color: var(--vp-c-brand-1);
}

.step-dot.done .dot {
  background: var(--vp-c-brand-1);
  border-color: var(--vp-c-brand-1);
  color: #fff;
}

.step-label {
  font-size: 0.75rem;
  color: var(--vp-c-text-3);
  white-space: nowrap;
}

.step-dot.active .step-label {
  color: var(--vp-c-text-1);
}

.step-line {
  width: 48px;
  height: 2px;
  background: var(--vp-c-divider);
  margin: 0 8px;
  margin-bottom: 22px;
  transition: background 0.3s;
}

.step-line.active {
  background: var(--vp-c-brand-1);
}

/* 选项区域 */
.options-panel {
  text-align: center;
}

.options-label {
  font-size: 1rem;
  font-weight: 500;
  color: var(--vp-c-text-1);
  margin: 0 0 1rem;
}

.options-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 10px;
}

.option-card {
  padding: 0.75rem 1rem;
  border-radius: 8px;
  border: 1px solid var(--vp-c-divider);
  background: var(--vp-c-bg-soft);
  color: var(--vp-c-text-1);
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
}

.option-card:hover {
  border-color: var(--vp-c-brand-2);
  background: var(--vp-c-brand-soft);
}

.option-card.selected {
  border-color: var(--vp-c-brand-1);
  background: var(--vp-c-brand-soft);
  color: var(--vp-c-brand-1);
}

/* 结果 */
.result-panel {
  text-align: center;
}

.result-label {
  font-size: 0.9rem;
  color: var(--vp-c-text-2);
  margin: 0 0 0.5rem;
}

.result-name {
  font-size: 1.75rem;
  font-weight: 700;
  color: var(--vp-c-brand-1);
  margin: 0 0 1.5rem;
}

.result-actions {
  display: flex;
  justify-content: center;
  gap: 12px;
  flex-wrap: wrap;
}

.btn-primary {
  display: inline-block;
  padding: 0.5rem 1.25rem;
  border-radius: 8px;
  font-weight: 500;
  font-size: 0.9rem;
  color: #fff;
  background: var(--vp-c-brand-1);
  text-decoration: none;
  transition: background 0.25s;
}

.btn-primary:hover {
  background: var(--vp-c-brand-2);
}

.btn-secondary {
  padding: 0.5rem 1.25rem;
  border-radius: 8px;
  font-weight: 500;
  font-size: 0.9rem;
  color: var(--vp-c-text-1);
  background: var(--vp-c-bg-soft);
  border: 1px solid var(--vp-c-divider);
  cursor: pointer;
  transition: border-color 0.25s;
}

.btn-secondary:hover {
  border-color: var(--vp-c-brand-2);
}

/* 过渡动画 */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* 响应式 */
@media (max-width: 480px) {
  .wizard { padding: 1.25rem; }
  .options-grid { grid-template-columns: 1fr; }
  .step-line { width: 24px; }
}
</style>
