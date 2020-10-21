<template>
  <div class="hello">
    <h1>
      <span>{{ time.hours }}:</span>
      <span>{{ time.minutes }}:</span>
      <span>{{ time.seconds }}</span>
    </h1>
  </div>
</template>

<script>
export default {
  name: "Clock",
  props: {
    time: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  grid-area: clock;
}
</style>
