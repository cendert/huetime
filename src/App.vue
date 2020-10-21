<template>
  <div id="app" v-bind:style="appStyle">
    <Clock v-bind:colors="colors" v-bind:time="time"/>
  </div>
</template>

<script>
import Clock from "./components/Clock";
// import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  data() {
    return {
      cursor: "auto",
      time: {},
      timeout: () => {
      },
      progress: {
        hours: 0,
        minutes: 0
      },
    };
  },
  components: {
    Clock,
    // HelloWorld,
  },
  computed: {
    appStyle: function () {
      return {
        backgroundColor: this.colors.hoursGrayscale,
        cursor: this.cursor,
      };
    },
    colors: function () {
      return {
        hoursColor: `hsl(
          ${this.progress.hours * 360},
          ${this.toTriangle(this.progress.hours) * 100}%,
          50%)`,
        hoursGrayscale: `hsl(
          0,
          0%,
          ${this.progress.hours * 360}%)`,
        minutesColor: `hsl(
          ${this.progress.minutes * 360},
          ${this.toTriangle(this.progress.minutes) * 100}%,
          50%)`,
      }
    }
  },
  methods: {
    showCursor() {
      clearTimeout(this.timeout);
      this.cursor = "auto";
      const hideCursor = () => {
        this.cursor = "none";
      };
      this.timeout = setTimeout(hideCursor, 3000);
    },
    toTriangle(progress) {
      const progressWithinThird = ((progress + 1 / 6) % (1 / 3)) * 3;
      const relativeProgress = 2 * progressWithinThird - 1;
      const formula = (relProgress) =>
          1 - 0.5 * Math.sqrt(1 - relProgress * relProgress);
      return formula(relativeProgress);
    },
    leftPad(str, len, ch) {
      str = String(str);
      var i = -1;
      if (!ch && ch !== 0) ch = " ";
      len = len - str.length;
      while (++i < len) {
        str = ch + str;
      }
      return str;
    },
    getProgress(time) {
      const {hours, minutes, seconds} = time;
      const hoursPart = parseInt(hours, 10) * 3600;
      const minutesPart = parseInt(minutes, 10) * 60;
      const secondsPart = parseInt(seconds, 10);
      const max = 24 * 3600;
      return {
        hours: (hoursPart + minutesPart + secondsPart) / max,
        minutes: (minutesPart / 3600)
      };
    },
    setTime() {
      const date = new Date();
      const time = {
        hours: this.leftPad(date.getHours(), 2, 0),
        minutes: this.leftPad(date.getMinutes(), 2, 0),
        seconds: this.leftPad(date.getSeconds(), 2, 0),
      };
      this.time = time;
      this.progress = this.getProgress(time);
    },
    tick() {
      setInterval(this.setTime, 1000);
    },
  },
  mounted() {
    this.tick();
    document.addEventListener("mousemove", this.showCursor);
  },
};
</script>

<style>
body {
  color: rgba(0, 0, 0, 0.4);
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 6vh;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

#app {
  background-color: #333;
  bottom: 0;
  display: grid;
  grid-template:
    ". . ." 1fr
    ". clock ." auto
    ". . ." 1fr
    / 1fr auto 1fr;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
}
</style>
