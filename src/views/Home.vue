<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import {
  // defineComponent 是 TypeScript 拿來封裝 setup hook 的一個方法
  // 透過這個方法可以讓 component 被正確地型別推斷
  defineComponent,
} from 'vue';

export default defineComponent({
  setup() {
    type text = string;
    const count:text = '1';
    console.log(count);
    return {
      count,
    };
  },
});
</script>
