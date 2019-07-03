<template>
  <div>
    <p>Test!</p>
    <p>{{ testData }}</p>
  </div>
</template>

<script>
export default {
  name: "Test.vue",
  data() {
    return {
      testData: "test data!"
    };
  }
};
</script>

<style scoped></style>
