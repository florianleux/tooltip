<template>
   <span class="ml-1 emoji">{{emoji}}</span>
</template>

<script>
export default {
  name: "EmojiGenerator",
  data: () => {
    return {
      emoji: "Pas d'emoji"
    }
  },
  mounted(){
    this.emoji = this.getRandomEmoji()
  },
  methods: {
   getRandomEmoji(){
     const emojis = ['😀','😃','😄','😁','😆','😅'];

      return emojis[~~(Math.random() * emojis.length)]

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
    right:50%;
    top: $tooltip-margin;
    transform: translate(-50%, -100%);
  }

  &.right {
    top:50%;
    right: $tooltip-margin;
    transform: translate(100%, -50%);
  }

  &.left {
    top:50%;
    left: $tooltip-margin;
    transform: translate(-100%, -50%);
  }

  &.bottom {
    right:50%;
    bottom: $tooltip-margin;
    transform: translate(50%, 100%);
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
