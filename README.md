# vue-form-el

> vue表单组件美化，包括radio、checkbox和swpier

## Build Setup

``` bash
# v-model：绑定值，label：初始值，isDisable：是否禁用
# checkbox多个复选框时，可以绑定到同一个数组

<radio v-model='radio' label='1' :isDisable='true'>radio1</radio>

<checkbox v-model='checkbox1'>checkbox1</checkbox>

<checkbox label='1' v-model='group'>checkbox1</checkbox>
<checkbox label='2' v-model='group'>checkbox2</checkbox>
<checkbox label='3' v-model='group'>checkbox3</checkbox>

<switch-el v-model='switch1'>switch1</switch-el>
```

## 预览

<a href="https://zhazhjie.github.io/vue-components-demo/?id=el">Demo</a>
