<template>
  <PageWrapper title="表单增删示例">
    <CollapseContainer title="表单增删">
      <BasicForm @register="register" @submit="handleSubmit">
        <template #add="{ field }">
          <AntButton v-if="Number(field) === 0" @click="add">+</AntButton>
          <AntButton v-if="field > 0" @click="del(field)">-</AntButton>
        </template>
      </BasicForm>
    </CollapseContainer>
  </PageWrapper>
</template>
<script lang="ts">
  import { defineComponent, ref } from 'vue'
  import { BasicForm, useForm } from '/@/components/Form/index'
  import { CollapseContainer } from '/@/components/Container/index'
  import { Input } from 'ant-design-vue'
  import { PageWrapper } from '/@/components/Page'
  import { Button as AntButton } from '/@/components/Button'

  export default defineComponent({
    components: { BasicForm, CollapseContainer, PageWrapper, [Input.name]: Input, AntButton },
    setup() {
      const [register, { appendSchemaByField, removeSchemaByFiled, validate }] = useForm({
        schemas: [
          {
            field: 'field0a',
            component: 'Input',
            label: '字段0',
            colProps: {
              span: 8
            },
            required: true
          },
          {
            field: 'field0b',
            component: 'Input',
            label: '字段0',
            colProps: {
              span: 8
            },
            required: true
          },
          {
            field: '0',
            component: 'Input',
            label: ' ',
            colProps: {
              span: 8
            },
            slot: 'add'
          }
        ],
        labelWidth: 100,
        actionColOptions: { span: 24 }
      })

      async function handleSubmit() {
        try {
          const data = await validate()
          console.log(data)
        } catch (e) {
          console.log(e)
        }
      }

      const n = ref(1)

      function add() {
        appendSchemaByField(
          {
            field: `field${n.value}a`,
            component: 'Input',
            label: '字段' + n.value,
            colProps: {
              span: 8
            },
            required: true
          },
          ''
        )
        appendSchemaByField(
          {
            field: `field${n.value}b`,
            component: 'Input',
            label: '字段' + n.value,
            colProps: {
              span: 8
            },
            required: true
          },
          ''
        )

        appendSchemaByField(
          {
            field: `${n.value}`,
            component: 'Input',
            label: ' ',
            colProps: {
              span: 8
            },
            slot: 'add'
          },
          ''
        )
        n.value++
      }

      function del(field) {
        removeSchemaByFiled([`field${field}a`, `field${field}b`, `${field}`])
        n.value--
      }

      return { register, handleSubmit, add, del }
    }
  })
</script>
