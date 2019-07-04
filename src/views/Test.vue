<template>
  <div>
    <p>{{ testData }}</p>
    <Charts></Charts>
  </div>
</template>

<script>
import Charts from '../components/Charts'
export default {
  name: 'Test.vue',
  components: { Charts },
  comments: {
    Charts
  },
  data() {
    return {
      testData: 'test data!'
    }
  }
}
</script>

<style scoped></style>
