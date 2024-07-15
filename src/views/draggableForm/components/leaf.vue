<template>
  <vue-draggable
    v-model="list"
    :group="{ name: 'display', pull: 'clone', put: false }"
    target=".display-item"
  >
    <div class="item-container" v-for="el in modelValue">
      <div>{{ el.label }}</div>
      <div class="display-item">
        <el-form-item :label="el.label">
          <el-input placeholder="请输入" />
        </el-form-item>
      </div>
    </div>
  </vue-draggable>
</template>

<script setup>
import { VueDraggable } from 'vue-draggable-plus'
import { defineProps, computed, defineEmits } from 'vue'
const props = defineProps({
  modelValue: Array,
})
const emit = defineEmits(['update:modelValue'])
const list = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val),
})
</script>

<style scoped lang="less">
.item-container {
  position: relative;
  .display-item {
    //position: absolute;
    //z-index: 1;
    //left: 0;
    //top: 0;
    //opacity: 0;
    //height: 21px;
    //overflow: hidden;
    /deep/.el-form-item {
      margin: 0;
      .el-form-item__label {
        height: 21px;
        line-height: 21px;
      }
    }
  }
}
</style>
