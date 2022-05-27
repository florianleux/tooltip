<template>
  <span class="relative">
 <transition name="fade" mode="out-in" appear>
       <div
           v-show="isVisible"
           :class="tooltipClass"
           class="tooltip absolute whitespace-nowrap bg-slate-700 text-white rounded px-2 py-1 "
           :style="`max-height:${tooltipMaxHeight}px; max-width:${tooltipMaxWidth}px`"
       >
      {{ text }}
    </div>
  </transition>

    <span ref="tooltip-target">
      <slot name="activator" :tooltip-handlers="tooltipHandlers" />
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
    let vm = this;
    return {
      isVisible: false,
      tooltipClass: 'top',
      tooltipMaxHeight: 0,
      tooltipMaxWidth: 0,
      tooltipHandlers:{}
    }
  },
  mounted(){
    //Initiating event handlers
    this.tooltipHandlers = {
      mouseover: this.showTooltip,
      focusin : this.showTooltip,
      mouseleave:  this.hideTooltip,
      focusout:  this.hideTooltip ,
    }

  },
  methods: {
    calculatePosition() {
      const targetPosition = this.$refs["tooltip-target"].getBoundingClientRect(),
          windowHeight = window.innerHeight,
          windowWidth = window.innerWidth;

      const remainingSpace = {
        "top": targetPosition.top,
        "right": windowWidth - targetPosition.right,
        "bottom": windowHeight - targetPosition.bottom,
        "left": targetPosition.left,
      }

      const maxSpaceDirection = Object.keys(remainingSpace).reduce((a, b) => remainingSpace[a] > remainingSpace[b] ? a : b);

      this.tooltipClass = maxSpaceDirection;
      this.tooltipMaxWidth = ['left', 'right'].includes(maxSpaceDirection) ? remainingSpace[maxSpaceDirection] / 2 : windowWidth / 2;
      this.tooltipMaxHeight = ['top', 'bottom'].includes(maxSpaceDirection) ? remainingSpace[maxSpaceDirection] / 2 : windowHeight / 2;
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
$tooltip-margin: -15px;

.tooltip {
  font-size: 0.8em;
  overflow: hidden;

  &.top {
    top: $tooltip-margin;
    transform: translate(0%, -100%);
  }

  &.right {
    right: $tooltip-margin;
    transform: translate(100%, 0);
  }

  &.left {
    bottom: $tooltip-margin;
    transform: translate(-100%, 0);
  }

  &.bottom {
    right: $tooltip-margin;
    transform: translate(0, 100%);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

</style>
