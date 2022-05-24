<template>
  <span class="relative" >
    <div
      v-show="isVisible"
      class="tooltip absolute whitespace-nowrap"
      :class="tooltipClass"
    >
      {{ text }}
    </div>
    <span ref="tooltip-target">
      <slot name="activator"  :show-tooltip="showTooltip" :hide-tooltip="hideTooltip"/>
    </span>
  </span>


</template>

<script>
export default {
  name: "Tooltip",
  props: {
    text: {type: String, required: true}
  },
  data: () => {
    return {
      isVisible: false,
      tooltipClass: 'top'
    }
  },
  mounted() {
    this.calculatePosition();

  },
  methods: {
    calculatePosition() {
      let targetPosition = this.$refs["tooltip-target"].getBoundingClientRect(),
          windowHeight = window.innerHeight,
          windowWidth = window.innerWidth;

      if(targetPosition.top > 2*windowHeight/3){
        this.tooltipClass = 'top'
      }else if(targetPosition.left < windowWidth/3) {
      this.tooltipClass = 'right'
      }else if(targetPosition.right > 2*windowWidth/3) {
      this.tooltipClass = 'left'
      }else if(targetPosition.bottom < windowWidth/3) {
      this.tooltipClass = 'bottom'
      }

    },
    hideTooltip() {
      this.isVisible = false;
    },
    showTooltip() {
      this.isVisible = true;

    }

  }

}
</script>

<style scoped lang="scss">
$tooltip-margin : -15px;

.tooltip {
  &.top{
    top:$tooltip-margin;
    transform: translate(0%,100%);
  }

  &.right{
    right: $tooltip-margin;
    transform: translate(100%,0);
  }

  &.left{
    bottom: $tooltip-margin;
    transform: translate(0%,-100%);
  }

  &.bottom{
    right: $tooltip-margin;
    transform: translate(-100%,0);
  }
}
</style>
