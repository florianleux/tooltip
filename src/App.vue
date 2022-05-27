<script lang="ts">
  import Tooltip from './components/Tooltip.vue'
  export default {
    name:"App",
    components:{Tooltip}
  }
</script>

<template>
  <div id="app" class="p-8">
    <Tooltip text="I'm a tooltip"  >
      <template v-slot:activator="{tooltipHandlers}">
        <button v-on="tooltipHandlers"> Click Me ! </button>
      </template>
    </Tooltip>
  </div>
</template>

<style lang="scss">
  @import "./styles/global.scss";
</style>
