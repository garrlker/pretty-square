<template>
  <div tabindex="0" class="hello" @keydown.ctrl.exact="changePerspective" @keydown.space="rotateMenu" @click="rotateMenu">
    <div class="scene">
      <div class="box" :style="boxRenderStyle">
        <div class="box-face box-face-front">front</div>
        <div class="box-face box-face-back">back</div>
        <div class="box-face box-face-right">right</div>
        <div class="box-face box-face-left">left</div>
        <div class="box-face box-face-top">top</div>
        <div class="box-face box-face-bottom">bottom</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Box",
  data() {
    return {
      x: -45,
      y: -45,
      z: 0,
      mode: 1,
      faceIndex: 0,
      faces: ["front", "left", "back", "right"]
    };
  },
  computed: {
    boxRenderStyle() {
      return {
        "--x-angle": `${this.x}deg`,
        "--y-angle": `${this.y}deg`,
        "--z-angle": `${this.z}deg`
      };
    },
    currentFace() {
      return this.faces[this.faceIndex];
    }
  },
  methods: {
    changePerspective(){
      if(this.mode){
        this.x += 45;
        this.y += 45;
      }else{
        this.x -= 45;
        this.y -= 45;
      }

      mode = !mode;
    },
    rotateMenu() {
      this.x += 90;

      this.faceIndex += 1;
      this.faceIndex %= 4;

      this.$emit("face", this.currentFace);
      // this.y += 90;
    }
  }
};
</script>

<style scoped lang="scss">
$side-length: calc((40vw + 40vh) / 2);
$opacity: 1;
$tweenSpeed: 0.2s ease;
$--x-angle: 0deg;
$--y-angle: 0deg;
$--z-angle: 0deg;

.hello {
  display: flex;
  width: 100vw;
  height: 100vh;

  .scene {
    width: $side-length;
    height: $side-length;
    perspective: 0px;
    margin: auto;
  }

  .box {
    width: $side-length;
    height: $side-length;
    transform-style: preserve-3d;
    transform: translateZ(calc( -(#{$side-length} - 50px)));
    transition: transform 1s;
  }

  .box-face {
    width: $side-length;
    height: $side-length;
    position: absolute;
    border: 2px solid black;
    font-size: 40px;
    font-weight: bold;
    color: white;
    text-align: center;
    user-select: none;
    border-radius: 0.5em;
  }

  .box-face-front,
  .box-face-back {
    line-height: $side-length;
  }

  .box-face-right,
  .box-face-left {
    left: 0px;
    line-height: $side-length;
  }

  .box-face-top,
  .box-face-bottom {
    top: 0px;
    line-height: $side-length;
  }

  .box-face-front {
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
  .box-face-right {
    background: linear-gradient(to top, #a18cd1 0%, #fbc2eb 100%);
  }
  .box-face-back {
    background: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
  }
  .box-face-left {
    background: linear-gradient(120deg, #f6d365 0%, #fda085 100%);
  }
  .box-face-top {
    background: linear-gradient(to top, #cfd9df 0%, #e2ebf0 100%);
  }
  .box-face-bottom {
    background: linear-gradient(to top, #30cfd0 0%, #330867 100%);
  }

  .box-face-front {
    transform: rotateY(var(--x-angle)) rotateX(var(--y-angle)) rotateY(0deg)
      translateZ(calc(#{$side-length} / 2));
    transition: transform $tweenSpeed;
  }
  .box-face-back {
    transform: rotateY(var(--x-angle)) rotateX(var(--y-angle)) rotateY(180deg)
      translateZ(calc(#{$side-length} / 2));
    transition: transform $tweenSpeed;
  }

  .box-face-right {
    transform: rotateY(var(--x-angle)) rotateX(var(--y-angle)) rotateY(90deg)
      translateZ(calc(#{$side-length} / 2));
    transition: transform $tweenSpeed;
  }
  .box-face-left {
    transform: rotateY(var(--x-angle)) rotateX(var(--y-angle)) rotateY(-90deg)
      translateZ(calc(#{$side-length} / 2));
    transition: transform $tweenSpeed;
  }

  .box-face-top {
    transform: rotateX(90deg) translateZ(calc(#{$side-length} / 2));
  }
  .box-face-bottom {
    transform: rotateX(-90deg) translateZ(calc(#{$side-length} / 2));
  }

  label {
    margin-right: 10px;
  }
}
</style>