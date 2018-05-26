## input组件
包含了
- input输入框
- radio单选项
- select下拉框
- textarea文本域
组件接受多个参数：
- type(optional)： 组件类型，包括textarea、select、radio，默认为text
- label(optional)：label项，显示在input之前
- value(require)：值
- name(optional)：name选项
- options：在`type`等于`select`或`radio`时为必须项。
- placeholder(optional)：原生属性
- required(optional)：原生属性，是否必填
### Usage 使用方法
上手即用，对不同类型的input，需绑定不同事件来监听值的改变。
``` html
<template>
  <v-input
    v-for="data in inputData"
    :key="data.name"
    v-bind="data"
    @input=data.value = $event
    @selectChange=data.vaule = $evnet
    @radioChange=data.value = $event>
</template>

<script>
  data() {
    return {
      inputData: [
        {
          label: '姓名',
          value: '',
          name: 'realName',
          placeholder: '请输入你的姓名'
        },
        {
          label: '公司性质',
          value: 'default',
          name: 'companyType',
          type: 'select',
          options: [
            {
              label: '请输入公司类型',
              value: 'default',
              disabled: true
            },
            {
              label: 'A类公司',
              value: 'a'
            },
            {
              label: 'B类公司',
              value: 'b'
            }
          ]
        }
      ]
    }
  }
</script>
```