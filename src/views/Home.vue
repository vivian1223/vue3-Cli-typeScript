<template lang="pug">
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
    // 透過 type 設定 input 的型別
    type input = {
      a:string
    }
    const email = ref<input>({ a: '請輸入' });
    // 使用 watch 時要注意：要監聽的值有所改變才會觸發 watch
    // 除了單純監聽某個物件的話，可以透過以下方式來進行監聽
    watch(email.value, (newValue, oldValue) => console.log(newValue, oldValue));
    // 如果想要進行物件內容的監聽
    // 一開始你可能會寫成
    // watch(email.value.a, (newValue, oldValue) => console.log(newValue, oldValue));
    // 但你會發現這樣會報錯：No overload matches this call.
    //   The last overload gave the following error.ts(2769)
    // runtime-core.d.ts(1902, 25): The last overload is declared here.
    // const email: Ref<{
    //     a: string;
    // }>
    // 如果要進行深層的監聽，watch 的第一個參數要使用 ()=> paylod 的方式來進行監聽
    watch(() => email.value.a, (newValue, oldValue) => console.log(newValue, oldValue));
    // 多值監聽
    // 如果要進行多值監聽的話，可以透過陣列的方式將值列舉出來
    // 對應的 newValue 及 oldValue 也可以參照位置，用陣列的方式列舉出來
    // 若要進行深層的監聽，可以透過在欲做深層監聽的部分使用 arrow function
    watch([() => email.value.a, email.value],
      ([aNewValue, emailNewValue], [aOldValue, emailOldValue]) => {
        console.log(aNewValue, emailNewValue, aOldValue, emailOldValue);
      });
    return { email };
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
