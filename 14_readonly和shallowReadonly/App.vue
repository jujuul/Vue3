<template>
  <h2>readonly和shallowReadonly</h2>
  <h3>state:{{ state }}</h3>
  <hr />
  <button @click="update">更新数据</button>
</template>
<script lang="ts">
import { defineComponent, reactive, readonly, ref, shallowReadonly } from "vue";
export default defineComponent({
  name: "App",
  setup() {
    // const state = reactive({
    //   name: "佐助",
    //   age: 20,
    //   car: {
    //     name: "Bench",
    //     color: "yellow",
    //   },
    // });
    const state = ref({
      name: "佐助",
      age: 20,
      car: {
        name: "Bench",
        color: "yellow",
      },
    });
    console.log(state);
    // 只读的数据---深度的只读
    // const state2 = readonly(state);
    // shallowReadonly---浅只读
    const state2 = shallowReadonly(state);
    const update = () => {
      // state2.name += "==";
      state2.value.car.name += "==";
    };

    return {
      state,
      update,
    };
  },
});
</script>
