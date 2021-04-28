<template>
  <h2>App父级组件</h2>
  <hr />
  <ModalButton />
</template>
<script lang="ts">
import ModalButton from "./ModalButton.vue";
import { defineComponent } from "vue";
export default defineComponent({
  name: "App",
  components: {
    ModalButton,
  },
});
</script>
