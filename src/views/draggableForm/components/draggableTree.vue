<template>
  <vue-draggable
    v-model="list"
    tag="ul"
    class="draggable-tree"
    :group="{ name: 'display', pull: 'clone', put: false }"
    handle=".leaf"
  >
    <!--    <div class="root-node" @click="toggleStatus" v-for="el in modelValue">-->
    <!--      <div :class="{'leaf'}">-->
    <!--        <el-icon v-if="el.children"><CaretRight /></el-icon>-->
    <!--        {{ el.label }}-->
    <!--      </div>-->
    <!--      <draggable-tree v-model="el.children" />-->
    <!--      <leaf v-model="el.children" />-->
    <!--    </div>-->
    <li
      class="root-node"
      v-for="el in modelValue"
      @click="toggleStatus"
      :key="el.id"
    >
      <p :class="{ leaf: !el.children }">
        <el-icon v-if="el.children"><CaretRight /></el-icon>
        {{ el.label }}
      </p>
      <draggable-tree v-model="el.children" />
    </li>
  </vue-draggable>
</template>

<script setup>
import { VueDraggable } from 'vue-draggable-plus'
import { computed } from 'vue'
import Leaf from '@/views/draggableForm/components/leaf.vue'
const props = defineProps({
  modelValue: Array,
})

const emit = defineEmits(['update:modelValue'])

const list = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val),
})

const toggleStatus = (e) => {
  let dom = e.target
  if (dom.className !== 'root-node') {
    dom = dom.parentNode
  }
  const status = dom.dataset.status
  dom.dataset.status = status === 'open' ? 'close' : 'open'
  const height = dom.scrollHeight
  dom.style.height = status === 'open' ? '21px' : height + 'px'
}
</script>

<style scoped lang="less">
.draggable-tree {
  list-style: none;

  svg {
    transition: all 0.3s ease;
  }

  .root-node {
    transition: all 0.3s ease;
    height: 21px;
    overflow: hidden;

    .leaf {
      padding-left: 20px;
    }
    &[data-status='close'] {
      height: 21px;
    }
    &[data-status='open'] {
      svg {
        transform: rotate(90deg);
      }
    }
  }
}
</style>
