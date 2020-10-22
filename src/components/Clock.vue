<template>
  <svg class="clock" viewBox="0 0 64 64">
    <defs>
      <filter id="shadow">
        <feDropShadow dx="0" dy="0" stdDeviation="2" v-bind:flood-color="colors.minutesColor"/>
      </filter>
    </defs>
    <circle class="clock-circle" r="24" cx="32" cy="32" v-bind:fill="colors.hoursColor" style="filter:url(#shadow);"/>
    <text class="time-part" x="32" y="32" font-size="8">
      <tspan class="time-part-hours">{{time.hours || '00'}}</tspan>
      <tspan class="separator">:</tspan>
      <tspan class="time-part-minutes">{{time.minutes || '00'}}</tspan>
      <tspan class="separator">:</tspan>
      <tspan class="time-part-seconds">{{time.seconds || '00'}}</tspan>
    </text>
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
@font-face {
  font-family: 'Droid Sans Mono';
  src: url('../../public/fonts/DroidSansMono.ttf')
}

.clock {
  grid-area: clock;
  max-height: 100vh;
  max-width: 100vw;
}

.time-part {
  fill: rgba(0, 0, 0, 0.4);
  font-family: "Droid Sans Mono", "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-anchor: middle;
  dominant-baseline: central;
  font-weight: 700;
}

.separator {
  font-family: sans-serif;
}
</style>
