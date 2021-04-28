<template>
  <div>Child子级组件</div>
  <h3>msg:{{ msg }}</h3>
  <button @click="emitXxx">分发事件</button>
</template>
<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "child",
  props: ["msg"],
  // setup细节问题
  // setup是在beforeCreate生命周期回调之前就执行了，而且就执行一次
  // 由此可以推断出：setup在执行的时候，当前的组件还没有创建出来，也就意味着：组件实例对象this根本不能用
  // this时undefined，说明不能通过this再去调用data/computed/methods中的相关内容
  // 其实所有的composition API相关回调函数中也都不可以

  // setup中的返回值是一个对象，内部的属性和方法是给html模板使用的
  // setup中的对象内部的属性和data函数中的return对象的属性都可以在html模板中使用
  // setup中的对象中的属性和data函数中的对象中的属性会合并为组件对象的属性
  // setup中的对象中的方法和methods对象中的方法会合并为组件对象的方法
  // 如果有重名, setup优先 **这条是错的，如有重名，会报错**
  // 在Vue3中尽量不要混合的使用data和setup以及methods和setup
  // 一般不要混合使用: methods中可以访问setup提供的属性和方法, 但在setup方法中不能访问data和methods
  // setup不能是一个async函数: 因为返回值不再是return的对象, 而是promise, 模板看不到return对象中的属性数据

  // 数据初始化的生命周期回调
  //   beforeCreate() {
  //     console.log("beforeCreate执行了");
  //   },
  setup(props, context) {
    // props参数，是一个对象，里面有父级组件向子级组件传递的数据，并且是在子级组件中使用props接收到的所有的属性
    // console.log(props.msg);
    // console.log(context.attrs);
    // console.log(context.emit);
    // context参数，是一个对象，里面有attrs对象（获取当前组件标签上的属性，但是该属性是在props中没有声明接收的所有的属性的对象，相当于$attrs），emit方法，slots对象
    console.log(context.attrs.msg2);
    console.log("setup执行了", this);
    const showMsg1 = () => {
      console.log("setup中的showMsg方法");
    };
    // 按钮的点击事件的回调函数
    function emitXxx() {
      context.emit("xxx", "++");
    }
    return {
      // setup中一般都是返回一个对象，对象中的属性和方法都可以在html模板中直接使用
      showMsg1,
      emitXxx,
    };
  },
  //   data() {
  //     return {
  //       count: 10,
  //     };
  //   },
  //   mounted() {
  //     console.log(this);
  //   },
  //   methods: {
  //     showMsg2() {
  //       console.log("methods中的showMsg方法");
  //     },
  //   },
});
</script>
