<template>
  <inline-svg v-if="svg!==''" :src="require('/src/assets/icon/'+svg+'.svg')"></inline-svg>
</template>

<script>
import InlineSvg from 'vue-inline-svg';
import Navigation from "@/components/shared/navigation";

export default {
  name: "app-icon",
  components: {Navigation, InlineSvg},
  props: {
    svg: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>

</style>