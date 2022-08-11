<template>
  <h2>当前的y是:{{ x.y }}</h2>
  <button @click="x = {y:888}">点我替换x</button>
  <button @click="x.y++">点我y+1</button>
  <hr/>
  <h4>{{ person }}</h4>
  <h2>姓名:{{ name }}</h2>
  <h2>年龄:{{ age }}</h2>
  <h2>薪资:{{ job.j1.salary }}</h2>
  <button @click="name = name + '~'">修改姓名</button>
  <button @click="age++">增长年龄</button>
  <button @click="job.j1.salary++">增长薪资</button>
</template>

<script>
import {ref, reactive, shallowReactive, shallowRef, toRefs} from "vue";

export default {
  name: "Demo",
  setup() {
    //shallowReactive只考虑对象类型的第一层数据响应式
    // let person = shallowReactive({
    //   name: '张三',
    //   age: 18,
    //   job: {
    //     j1: {
    //       salary: 20
    //     }
    //   }
    // });

    let person = reactive({
      name: '张三',
      age: 18,
      job: {
        j1: {
          salary: 20
        }
      }
    });

    //传递基本类型来说,ref和shallowRef基本是没什么区别
    // let x = ref(0);
    // let x = shallowRef(0);
    //但注意对象类型shallowRef不去处理,而ref底层会去借助reactive生成proxy对象(getter/setter)
    //但注意不管是shallow还是非shallow,第一层都是响应式的(如下面的x依然是响应式数据)
    // let x = ref({y: 0});
    let x = shallowRef({y: 0});
    console.log(x);

    return {
      person,
      ...toRefs(person),
      x
    }

  }
}
</script>

<style>

</style>