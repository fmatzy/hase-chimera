<template>
  <ChimeraField/>
</template>

<script lang="ts">
import {
  Component,
  Vue
} from "nuxt-property-decorator"
import ChimeraField from "~/components/ChimeraField.vue"

@Component({
  components: {
    ChimeraField
  }
})
export default class extends Vue {
}
</script>
