<template>
  <div class="p-5">
    多层级缓存-页面2
    <br />
    <AntInput />
  </div>
</template>
<script lang="ts">
  import { defineComponent } from 'vue'
  import { Input as AntInput } from 'ant-design-vue'
  export default defineComponent({
    name: 'Menu2Demo',
    components: { AntInput }
  })
</script>
