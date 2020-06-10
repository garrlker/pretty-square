<template>
  <div id="box" :class="[backgroundClass]">
    <Box @face="setClass" />
  </div>
</template>

<script>
import Box from "./components/Box.vue";

export default {
  name: "App",
  components: {
    Box
  },
  data() {
    return {
      backgroundClass: "front"
    };
  },
  methods: {
    setClass(newClass) {
      this.backgroundClass = newClass;
    }
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
  width: 100vw;
  height: 100vh;
}
#box {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  transition: background 0.2s ease;

  &.front {
    background: linear-gradient(
      to right,
      #ff8177 0%,
      #ff867a 0%,
      #ff8c7f 21%,
      #f99185 52%,
      #cf556c 78%,
      #b12a5b 100%
    );
  }
  &.back {
    background: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
  }
  &.left {
    background: linear-gradient(120deg, #f6d365 0%, #fda085 100%);
  }
  &.right {
    background: linear-gradient(to top, #a18cd1 0%, #fbc2eb 100%);
  }
  &.top {
    background: linear-gradient(to top, #cfd9df 0%, #e2ebf0 100%);
  }
  &.bottom {
    background: linear-gradient(to top, #30cfd0 0%, #330867 100%);
  }
}
</style>
