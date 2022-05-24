<script lang="ts">
  import Tooltip from './components/Tooltip.vue'
  export default {
    name:"App",
    components:{Tooltip}
  }
</script>

<template>
  <Tooltip text="I'm a tooltip"  >
    <template v-slot:activator="{showTooltip,hideTooltip}">
      <button @mouseover="showTooltip" @mouseleave="hideTooltip"> Click Me ! </button>
    </template>
  </Tooltip>
</template>

<style lang="scss">
  @import "./styles/global.scss";
</style>
