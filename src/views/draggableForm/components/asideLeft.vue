<template>
  <div class="aside-left-container common-panel">
    <header>模板选择</header>
    <draggable-tree v-model="list" />
  </div>
</template>

<script setup>
import { VueDraggable } from 'vue-draggable-plus'
import { ref } from 'vue'
import DraggableTree from '@/views/draggableForm/components/draggableTree.vue'

const defaultProps = {
  children: 'children',
  label: 'label',
}

const list = ref([
  {
    label: '输入',
    children: [
      { label: 'input', type: 'input333' },
      { label: 'textarea', type: 'textarea' },
    ],
  },
  {
    label: '选择',
    children: [
      { label: '单选', type: 'select' },
      { label: '多选', type: 'select-multiple' },
    ],
  },
  { label: '上传', children: [{ label: 'uploader', type: 'upload' }] },
])
</script>

<style scoped lang="less">
@import '/src/style/draggableForm/asideLeft.less';
</style>
