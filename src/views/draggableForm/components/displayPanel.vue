<template>
  <div class="display-panel-container common-panel">
    <el-form :model="form">
      <vue-draggable
        class="draggable-box"
        v-model="list"
        group="display"
        @update="onUpdate"
        @add="onAdd"
      >
        <el-form-item
          v-for="(item, index) in list"
          :key="index"
          :prop="item.prop"
          :label="item.label"
          :class="{ active: item.active }"
          :style="`width: ${item.width || 200}px`"
          @click="handleClick($event, item)"
        >
          <component
            is="el-input"
            placeholder="请输入"
            v-model="item.value"
            :disabled="true"
          ></component>
        </el-form-item>
      </vue-draggable>
    </el-form>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import { VueDraggable } from 'vue-draggable-plus'
import { v4 as uuidv4 } from 'uuid'

const emit = defineEmits(['clickItem', 'onAdd'])

const form = ref({})
const props = defineProps({
  list: Array,
})
let list = ref([])
watch(
  props.list,
  (val) => {
    list = val
  },
  { immediate: true, deep: true },
)
// 点击显示表单项
const handleClick = (e, item) => {
  e.preventDefault()
  emit('clickItem', item)
}
function onUpdate(e) {
  console.log(e)
}
function onAdd(e) {
  const data = e.clonedData
  data.id = uuidv4()
  emit('onAdd', data)
}
</script>

<style scoped lang="less">
@import '/src/style/draggableForm/displayPanel.less';
</style>
