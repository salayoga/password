# yj-psw

## Install

npm:

```js
npm install yj-psw --save
```

yarn:

```js
yarn add yj-psw
```

### Compiles and hot-reloads for development

```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Customize configuration
- This is a password entry box component, after installing,you can use it like input component,only allow input Number;

#### Use

```vue
<template>
  <div class="home">
      <yj-psw v-model="value"></yj-psw>
  </div>
</template>

<script>
import YjPsw from "@/components/psw"
export default {
  components: {
    YjPsw
  },
  data(){
    return {
      value:""
    }
  },
}
</script>
```

#### params

支持的参数：

| 参数名      | 参数作用         | 参数类型 | 默认值 |
| ----------- | ---------------- | -------- | ------ |
| num         | 密码框的个数     | Number   | 6      |
| width       | 密码框的长度     | Number   | 25     |
| borderColor | 密码框的边框颜色 | String   | #ccc   |

#### views

默认情况

![1599286351579](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1599286351579.png)

获取焦点

![1599286412648](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1599286412648.png)

正在输入

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1599286545287.png)

输入完成

![1599286520809](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1599286520809.png)

