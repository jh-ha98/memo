<template>
  <n-data-table :data="data" :columns="columns" :pagination="pagination" :single-line="false" />
  <div>d</div>
</template>

<script setup lang="ts">
import { NDataTable } from 'naive-ui'
import { h } from 'vue';
import DivideCols from './DivideCols.vue'
function createData() {
  return Array.from({ length: 50 }).map((_, i) => {
    return {
      key: i,
      name: `name_${i}`,
      physicsAttack: `physicsAttack_${i}`,
      magicAttack: `magicAttack_${i}`,
      defend: `defend_${i}`,
      speed: `speed_${i}`
    }
  })
}

const columns = [
  {
    title: 'Name',
    key: 'name'
  },
  {
    title: 'Attrs',
    key: 'attrs',
    children: [
      {
        title: 'Attack',
        key: 'attack',
        children: [
          {
            title: 'Physics Attack',
            key: 'physicsAttack',
            className: 'p-0 h-1 pl-1',
          },
          {
            title: 'Magic Attack',
            key: 'magicAttack',
            className: 'p-0 h-1 pl-1',
          }
        ]
      },
      {
        title: 'Defend',
        key: 'defend',
        className: 'p-0 h-1',
        render(row: any) {
          // return h(DivideCols, { left: row.defend, right: row.speed })
          return h('div', { class: 'd-flex hp-100' }, [
            h('div', { class: ' pl-1 rate-50 d-flex hp-100 item-center boarder-r' }, row.defend),
            h('div', { class: ' pl-1 rate-50 d-flex hp-100 item-center' }, row.speed)
          ])
        }
      },
      {
        title: 'Speed',
        key: 'speed',
        className: 'p-0 h-1 pl-1',
      }
    ]
  }
];
const pagination = { pageSize: 10 };
const data = createData();
</script>

<style scoped>
:deep(.p-0) {
  padding: 0;
}

:deep(.pl-1) {
  padding-left: 1rem;
}

:deep(.h-1) {
  height: 1rem;
}

:deep(.hp-100) {
  height: 100%;
}

:deep(.boarder-r) {
  border-right: 1px solid rgba(239, 239, 245, 1);
}

:deep(.d-flex) {
  display: flex;
}

:deep(.item-center) {
  align-items: center;
}

:deep(.rate-50) {
  flex: 1;
}
</style>