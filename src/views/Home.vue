<template lang="pug">
table
  thead
    tr
      td.table__thead 用戶編號
      td.table__thead 用戶名稱
      td.table__thead 會員等級
      td.table__thead 消費額度
  tbody
    tr
      td.table__tbody 0000001
      td.table__tbody 黃小明
      td.table__tbody 黃金
      td.table__tbody 12304
</template>

<script lang="ts">
import {
  // defineComponent 是 TypeScript 拿來封裝 setup hook 的一個方法
  // 透過這個方法可以讓 component 被正確地型別推斷
  defineComponent,
  ref,
} from 'vue';

export default defineComponent({
  setup() {
    // type text = string;
    const count = ref({ value: 1 });
    return {
      count,
    };
  },
});
</script>
<style lang="sass" scoped>
.table__text
  font-size: 1rem
  padding: 1.5rem 2rem
  border: 1px #e0e0e0 solid

.table__thead
  @extend .table__text
  background-color: #f8f9fb
  font-weight: bold
  color: #626262

.table__tbody
  @extend .table__text

</style>
