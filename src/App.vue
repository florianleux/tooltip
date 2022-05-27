<script lang="ts">
  import EmojiGenerator from './components/EmojiGenerator.vue'
  import Tooltip from './components/Tooltip.vue'
  export default {
    name:"App",
    components:{
      EmojiGenerator,
      Tooltip
    }
  }
</script>

<template>
  <div id="app" class="p-8 grid grid-cols-3 gap-4">
    <div class="p-8">
      <Tooltip>
        <template #content>
          <span>I'm a tooltip !</span>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" v-on="tooltipHandlers">Button</button>
        </template>
      </Tooltip>
    </div>
    <div class="p-8">
      <Tooltip>
        <template #content>
          <span>I'm a <b>tooltip</b> with <span class="text-green-400">HTML</span> inside !</span>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" v-on="tooltipHandlers">Button</button>
        </template>
      </Tooltip>
    </div>
    <div class="p-8">
      <Tooltip>
        <template #content>
          <span>I'm a tooltip with a vue Component inside !</span>
          <EmojiGenerator/>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <button class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded" v-on="tooltipHandlers">Button</button>
        </template>
      </Tooltip>
    </div>
    <div class="p-8">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        Username
      </label>
      <Tooltip>
        <template #content>
          <span>I'm a tooltip!</span>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Username" v-on="tooltipHandlers">
        </template>
      </Tooltip>

    </div>

    <div class="p-8">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        Username
      </label>
      <Tooltip>
        <template #content>
          <span>I'm a tooltip with a vue Component inside !</span>
          <EmojiGenerator/>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Username" v-on="tooltipHandlers">
        </template>
      </Tooltip>
    </div>

    <div class="p-8">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="username">
        Username
      </label>
      <Tooltip>
        <template #content>
          <span>I'm a <b>tooltip</b> with <span class="text-green-400">HTML</span> inside !</span>
        </template>
        <template v-slot:activator="{tooltipHandlers}">
          <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Username" v-on="tooltipHandlers">
        </template>
      </Tooltip>
    </div>

  </div>
</template>

<style lang="scss">
  @import "./styles/global.scss";
</style>
