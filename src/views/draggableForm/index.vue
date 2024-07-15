<template>
  <div class="draggable-form-container">
    <aside-left />

    <display-panel
      :list="displayList"
      @clickItem="chooseDisplayItem"
      @on-add="addDisplayItem"
    />

    <aside-right
      ref="schemaForm"
      :active-item="activeItem"
      @changLayoutForm="changLayoutForm"
      @changComForm="changComForm"
    />
  </div>
</template>

<script setup>
import AsideLeft from '@/views/draggableForm/components/asideLeft.vue'
import DisplayPanel from '@/views/draggableForm/components/displayPanel.vue'
import AsideRight from '@/views/draggableForm/components/asideRight.vue'
import { ref } from 'vue'
import { v4 as uuidv4 } from 'uuid'

const displayList = ref([])

const addDisplayItem = (item) => {
  displayList.value.push(item)
}

const deleteDisplayItem = (index) => {
  displayList.value.splice(index, 1)
}

const editDisplayItem = (index, data) => {
  for (let k in data) {
    displayList.value[index][k] = data[k]
  }
}

addDisplayItem({
  label: '姓名',
  type: 'input',
  id: uuidv4(),
})
addDisplayItem({
  label: '姓名2',
  type: 'input',
  id: uuidv4(),
})

// schemaForm配置组件
const schemaForm = ref(null)

// 选中显示表单项
const activeItem = ref(null)

const chooseDisplayItem = (item) => {
  const current = displayList.value.find((i) => i.id === item.id)
  displayList.value.forEach((item) => (item.active = false))
  current.active = true
  activeItem.value = current
  schemaForm.value.changeValue(current)
}

// 右侧布局表单改变
const changLayoutForm = (val) => {}
// 右侧组件表单改变
const changComForm = (val) => {
  if (activeItem.value) {
    editDisplayItem(
      displayList.value.findIndex((i) => i.id === activeItem.value.id),
      val,
    )
  }
}
</script>

<style scoped lang="less">
@import '/src/style/draggableForm/index.less';
</style>
