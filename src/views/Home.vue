<template lang="pug">
table
  thead
    tr
      td.table__thead {{ theadInfo.id }}
      td.table__thead {{ theadInfo.name }}
      td.table__thead {{ theadInfo.rank }}
      td.table__thead {{ theadInfo.quota }}
  tbody
    tr
      td.table__tbody 0000001
      td.table__tbody 黃小明
      td.table__tbody 黃金
      td.table__tbody 12304
input(v-model="email.a")
pre {{ email }}
</template>

<script lang="ts">
import {
  // defineComponent 是 TypeScript 拿來封裝 setup hook 的一個方法
  // 透過這個方法可以讓 component 被正確地型別推斷
  defineComponent,
  reactive,
  ref,
  watch,
} from 'vue';

export default defineComponent({
  setup() {
    // 透過 interface 宣告等等 reactive 會用到的型別定義
    interface thead {
      id: string,
      name: string,
      rank: string,
      quota: string
    }
    // reactive 是以 proxy 為基底實作出來的方法，所以只能透過 reactive 宣告物件型別的變數
    // 沒有透過 reactive 宣告的物件，會因為缺乏 getter 與 setter 而沒有辦法進行雙向綁定
    const theadInfo = reactive<thead>({
      id: '用戶編號',
      name: '用戶名稱',
      rank: '會員等級',
      quota: '消費額度',
    });
    // 透過 type 設定 input 的型別
    type input = {
      a:string
    }
    //  ref 定義物件型別
    // 這裡要注意的的是 ref 沒有辦法被直接覆蓋，不然會失去雙向綁定的功能
    // 如果要針對 ref 來重新賦值，要透過 email.value = xxx 的方式來進行改變值的動作
    const email = ref<input>({ a: '請輸入' });
    watch(email.value, (newValue, oldValue) => console.log(newValue, oldValue));
    // 所有需要提供模板或是外層取用的變數、函式都要 return 出去
    return { theadInfo, email };
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
