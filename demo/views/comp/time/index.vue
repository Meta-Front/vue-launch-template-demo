<template>
  <PageWrapper title="时间组件示例">
    <CollapseContainer title="基础示例">
      <CustomTime :value="time1" />
      <br />
      <CustomTime :value="time2" />
    </CollapseContainer>

    <CollapseContainer title="定时更新" class="my-4">
      <CustomTime :value="now" :step="1" />
      <br />
      <CustomTime :value="now" :step="5" />
    </CollapseContainer>

    <CollapseContainer title="定时更新">
      <CustomTime :value="now" mode="date" />
      <br />
      <CustomTime :value="now" mode="datetime" />
      <br />
      <CustomTime :value="now" />
    </CollapseContainer>
  </PageWrapper>
</template>
<script lang="ts">
  import { defineComponent, reactive, toRefs } from 'vue'
  import { PageWrapper } from '/@/components/Page'
  import { CustomTime } from '/@/components/Time'
  import { CollapseContainer } from '/@/components/Container/index'

  export default defineComponent({
    components: { PageWrapper, CustomTime, CollapseContainer },
    setup() {
      const now = new Date().getTime()
      const state = reactive({
        time1: now - 60 * 3 * 1000,
        time2: now - 86400 * 3 * 1000
      })
      return {
        ...toRefs(state),
        now
      }
    }
  })
</script>
