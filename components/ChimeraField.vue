<template>
  <div class="field" @click="createChimera">
    <Chimera v-for="(chimera, i) in chimeras" :key="i" :chimera="chimera"/>
  </div>
</template>

<script lang="ts">
import {
  Component,
  Vue
} from "nuxt-property-decorator"
import Chimera from "~/components/Chimera.vue"

@Component({
  components: {
    Chimera
  }
})
export default class ChimeraField extends Vue {
  chimeras: {x: number, y: number}[] = [];

  createChimera(evt: MouseEvent): void {
    this.chimeras.push({
      x: evt.x,
      y: evt.y,
    });
  }
}
</script>
<style lang="scss" scoped>
.field {
  position: fixed;
  width: 100%;
  height: 100%;
}
</style>
