<template>
  <span class="relative" >
    <div
      v-show="isVisible"
      :class="tooltipClass"
      class="tooltip absolute whitespace-nowrap"
      :style="`max-height:${tooltipMaxHeight}px; max-width:${tooltipMaxWidth}px`"
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
      tooltipClass: 'top',
      tooltipMaxHeight:0,
      tooltipMaxWidth: 0,
    }
  },
  methods: {
    calculatePosition() {
      const targetPosition = this.$refs["tooltip-target"].getBoundingClientRect(),
          windowHeight = window.innerHeight,
          windowWidth = window.innerWidth;

      const remainingSpace = {
            "top": targetPosition.top,
            "right":     windowWidth - targetPosition.right,
            "bottom": windowHeight - targetPosition.bottom,
            "left": targetPosition.left,
          }

      const maxSpaceDirection = Object.keys(remainingSpace).reduce((a, b) => remainingSpace[a] > remainingSpace[b] ? a : b);

      this.tooltipClass = maxSpaceDirection;
      this.tooltipMaxWidth = ['left','right'].includes(maxSpaceDirection) ? remainingSpace[maxSpaceDirection]/2 : windowWidth/2;
      this.tooltipMaxHeight = ['top','bottom'].includes(maxSpaceDirection) ? remainingSpace[maxSpaceDirection]/2 : windowHeight/2;
      },
    hideTooltip() {
      this.isVisible = false;
    },
    showTooltip() {
      this.calculatePosition();
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
    transform: translate(0%,-100%);
  }

  &.right{
    right: $tooltip-margin;
    transform: translate(100%,0);
  }

  &.left{
    bottom: $tooltip-margin;
    transform: translate(-100%,0);
  }

  &.bottom{
    right: $tooltip-margin;
    transform: translate(0,100%);
  }
}
</style>
