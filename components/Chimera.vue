<template>
  <div :style="position" class="chimera" :class="{touched: touched, inverse: inverse}"
    @click.stop="touch">
    <img ref="img" :src="imgSrc">
    <audio ref="audio" :src="audioSrc" preload="true"/>
  </div>
</template>
<script lang="ts">
import {
  Component,
  Prop,
  Vue
} from "nuxt-property-decorator"
import { setTimeout, setInterval } from "timers";

@Component({})
export default class Chimera extends Vue {
  @Prop() chimera: {x: number, y:number};

  readonly imgSrc = require("~/assets/hase_chimera.png");
  readonly imgSize: {width: number, height: number} = {width: 160, height: 160};

  readonly audioSrc = require("~/assets/hase_chimera.mp3");
  
  touched: boolean = false;
  inverse: boolean = false;

  get position() {
    return {
      top: (this.chimera.y - this.imgSize.height / 2) + 'px',
      left: (this.chimera.x - this.imgSize.width / 2) + 'px',
      position: "absolute",
    }
  }

  mounted(): void {
    setInterval(() => {
      const getDelta = () => Math.floor(Math.random() * 100) - 50;
      var deltaX = getDelta();
      var deltaY = getDelta();

      this.chimera.x += deltaX;
      this.chimera.y += deltaY;
      this.inverse = (deltaX > 0);
    },300);
  }

  touch(): void {
    if (this.touched) return;

    (this.$refs.audio as HTMLAudioElement).play();
    this.touched = true;
    setTimeout(() => { this.touched = false }, 1100);
  }

}
</script>
<style lang="scss" scoped>
.chimera {
  transition: top 0.3s, left 0.3s;
  -webkit-touch-callout: none;
  -webkit-user-select: none;

  &.touched {
    animation: fluffy 0.7s linear 0s 1;
  }
  &.inverse {
    transform: scale(-1,1);
  }
}

@keyframes fluffy {
  0%   { transform: scale(1.0, 1.0) translate(0%, 0%); }
  10%  { transform: scale(1.1, 0.9) translate(0%, 5%); }
  40%  { transform: scale(1.2, 0.8) translate(0%, 15%); }
  50%  { transform: scale(1.0, 1.0) translate(0%, 0%); }
  60%  { transform: scale(0.9, 1.2) translate(0%, -50%); }
  75%  { transform: scale(0.9, 1.2) translate(0%, -20%); }
  85%  { transform: scale(1.2, 0.8) translate(0%, 15%); }
  100% { transform: scale(1.0, 1.0) translate(0%, 0%); }
}
</style>
