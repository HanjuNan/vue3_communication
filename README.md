## 完整引入element-plus
- https://element-plus.gitee.io/zh-CN/guide/quickstart.html

## 尤大建议不要省略vue扩展名
- https://github.com/vitejs/vite/issues/178#issuecomment-630138450

- npm i less less-loader

- npm i pubsub-js @types/pubsub-js

- npm i @element-plus/icons-vue


# 组件通信总结

## 关于@click
在Vue2中直接在组件上@click是自定义事件,可以通过.native修饰符变成原始的DOM事件
vue3框架下,不管是在原生DOM上的@click还是组件上的@click都是原生DOM事件
只有当子组件通过$emits触发,这个时候在组件身上的@click才被认为是自定义事件

v-model指令: 收集表单数据,数据双向绑定
v-model也可以实现组件之间的通讯,实现父子组件数据同步的业务
父给子组件数据 props
子组件给父组件数据 自定义事件 

## 关于v-model
<Child v-model="money"></Child>

 v-model组件身上使用
第一:相当有给子组件传递props[modelValue] = 10000
第二:相当于给子组件绑定自定义事件update:modelValue

这种v-model在Elment Plus中会使用到，用来实现父子组件数据同步
<el-pagination
  v-model:current-page="currentPage2"
  v-model:page-size="pageSize2"
  :page-sizes="[100, 200, 300, 400]"
  :small="small"
  :disabled="disabled"
  :background="background"
  layout="sizes, prev, pager, next"
  :total="1000"
  @size-change="handleSizeChange"
  @current-change="handleCurrentChange"
/>
## $attrs和props
两者都可以拿到自定义属性
props优先级更高
props接收的属性,则$attrs中不接收

并且$attrs可以拿到自定义事件

## ref和$parents
组件内容数据默认是对外关闭的,即使拿到了组件实例也拿不到数据
如果想让外部访问需要通过defineExpose方法对外暴露

