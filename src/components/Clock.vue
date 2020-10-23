<template>
  <svg class="clock" viewBox="0 0 64 64">
    <defs>
      <filter id="shadow">
        <feDropShadow dx="0" dy="0" stdDeviation="2" v-bind:flood-color="colors.minutesColor"/>
      </filter>
    </defs>
    <circle class="clock-circle" r="24" cx="32" cy="32" v-bind:fill="colors.hoursColor" @click="click" style="filter:url(#shadow);"/>
    <text class="time-part" v-bind:class="{'show-time-part' : showTimePart}" x="32" y="32" font-size="8">
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
    click: Function,
    colors: Object,
    showTimePart: Boolean,
    time: Object,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@500&display=swap');

.clock {
  grid-area: clock;
  max-height: 100vh;
  max-width: 100vw;
  height: 100vh;
  width: 100vw;
}

.clock-circle {
  cursor: pointer;
}

.show-time-part {
  opacity: 0;
}

.time-part {
  fill: rgba(0, 0, 0, 0.4);
  font-family: "Roboto Mono", monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-anchor: middle;
  transition: opacity 1s ease-out;
  dominant-baseline: central;
  font-weight: 700;
  user-select: none;
  pointer-events: none;
}

.separator {
  font-family: sans-serif;
}
</style>
