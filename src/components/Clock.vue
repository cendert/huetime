<template>
  <svg class="clock" viewBox="0 0 64 64">
    <defs>
      <filter id="shadow">
        <feDropShadow dx="0" dy="0" stdDeviation="2" v-bind:flood-color="colors.minutesColor"/>
      </filter>
    </defs>
    <circle class="clock-circle" r="24" cx="32" cy="32" v-bind:fill="colors.hoursColor" style="filter:url(#shadow);"/>
    <text class="time-part" x="32" y="32" font-size="9">{{`${time.hours || '00'}:${time.minutes || '00'}:${time.seconds || '00'}`}}</text>
  </svg>
</template>

<script>
export default {
  name: "Clock",
  props: {
    colors: Object,
    time: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.clock {
  grid-area: clock;
  max-height: 100vh;
  max-width: 100vw;
}

.time-part {
  fill: rgba(0, 0, 0, 0.4);
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-anchor: middle;
  dominant-baseline: central;
  font-weight: 700;
}
</style>
