<template>
  <div>
    <h1 class="text-3xl font-bold underline bg-orange-500 p-10">Hello World</h1>
  </div>
  <Counter :year="2023" :month="8" :date="10" :hour="12" :minute="1" :second="1" :millisecond="1"/>
</template>

<script>
import Counter from "../components/Counter.vue";

export default {
  components: { Counter },
};
</script>

<style scoped></style>
