<template>
  <div class="aside-right-container common-panel">
    <el-tabs v-model="activeName" class="demo-tabs">
      <el-tab-pane label="表单" name="form">
        <el-form :form="form">
          <el-form-item label="布局">
            <el-radio-group v-model="form.layout" @change="handleFormChange">
              <el-radio-button
                v-for="item in layouts"
                :label="item.label"
                :value="item.value"
              />
            </el-radio-group>
          </el-form-item>
          <el-form-item label="尺寸">
            <el-radio-group v-model="form.size" @change="handleFormChange">
              <el-radio-button
                v-for="item in sizes"
                :label="item.label"
                :value="item.value"
              />
            </el-radio-group>
          </el-form-item>
        </el-form>
      </el-tab-pane>
      <el-tab-pane label="组件" name="component">
        <el-form :form="comForm">
          <el-form-item v-for="item in comFormItems" :label="item.label">
            <el-input
              v-if="item.type === 'numberInput'"
              clearable
              v-model.number="comForm[item.prop]"
              @change="handleComFormChange"
            >
              <template #append v-if="item.append">{{ item.append }}</template>
            </el-input>
            <el-input
              v-if="item.type === 'input'"
              clearable
              v-model="comForm[item.prop]"
              @change="handleComFormChange"
            />
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script setup>
import { VueDraggable } from 'vue-draggable-plus'
import { ref } from 'vue'

const props = defineProps({
  activeItem: Object,
})
const emit = defineEmits(['changLayoutForm', 'changComForm'])

const activeName = ref('form')
const layouts = [
  { label: '水平', value: 'horizontal' },
  { label: '对称', value: 'symmetric' },
]

const sizes = [
  { label: '小', value: 'small' },
  { label: '中', value: 'medium' },
  { label: '大', value: 'large' },
]

const form = ref({
  layout: 'horizontal',
  size: 'medium',
})
const handleFormChange = () => {
  emit('changLayoutForm', form.value)
}

const comFormItems = [
  { label: '宽', prop: 'width', type: 'numberInput', append: 'px' },
  { label: '标签', prop: 'label', type: 'input' },
  { label: '内容', prop: 'value', type: 'input' },
]
const comForm = ref({
  width: 200,
  label: '',
  value: '',
})
const handleComFormChange = () => {
  emit('changComForm', comForm.value)
}

const list = ref([
  { label: 'input', type: 'input' },
  { label: 'textarea', type: 'textarea' },
])

// form表单回显
const changeValue = (val) => {
  comForm.value = {
    width: val.width || 200,
    label: val.label || '',
    value: val.value || '',
  }
  // form
}

defineExpose({
  changeValue,
})
</script>

<style scoped lang="less">
@import '/src/style/draggableForm/asideRight.less';
</style>
