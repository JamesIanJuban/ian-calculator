<template>
  <div class="flex justify-between" 
    style="-webkit-app-region: drag;">
  <button @click="toggleHistory" 
    class="flex items-left ml-2 h-4 space-x-4 mt-2 transition duration-300 ease-in-out transform hover:scale-110">
  <MenuSvg class="w-10 h-8" />
  </button>
  <HistoryWindow v-if="historyVisible" 
    :show="historyVisible" 
    :history="historyData" 
    @toggle="toggleHistory" 
    @clear-history="clearHistory" />
  <div class="flex space-x-4 mr-4">

  <button class="text-gray-500 hover:text-gray-700 mt-2 focus:outline-none" 
    @click="minimize">
 
  </button>

  <button class="text-gray-500 hover:text-gray-700 mt-2 focus:outline-none" 
    @click="maximizeOrRestore">
  <svg v-if="!isMaximized"
    class="h-5 w-5" 
    fill="none"
    viewBox="0 0 24 24"
    stroke="currentColor">
  <path stroke-linecap="round" 
    stroke-linejoin="round" 
    stroke-width="2" 
    d="M6 6h12v12H6z"></path>
  </svg>
  <svg v-else class="h-5 w-5" 
    fill="none" 
    viewBox="0 0 24 24" 
    stroke="currentColor">
  <path stroke-linecap="round" 
    stroke-linejoin="round" 
    stroke-width="2" 
    d="M4 4h16v16H4z"></path>
  </svg>
  </button>

  <button class="text-gray-500 hover:text-gray-700 mt-2 focus:outline-none" 
    @click="close">
  <svg class="h-5 w-5" 
    fill="none" 
    viewBox="0 0 24 24" 
    stroke="currentColor">
  <path stroke-linecap="round"
    stroke-linejoin="round" 
    stroke-width="2" 
    d="M6 18L18 6M6 6l12 12"></path>
  </svg>
  </button>
  
  </div>
  </div>
</template>

<script>
import MenuSvg from './svg/MenuSvg.vue';
import HistoryWindow from './HistoryWindow.vue';

export default {
  name: 'AppBar',
  components: {
       MenuSvg,
       HistoryWindow,
  },
  props: {
    historyData: {
       type: Array,
       required: true,
    },
  },
  data() {
    return {
       historyVisible: false,
       isMaximized: false,
    };
  },
  methods: {
    toggleHistory() {
        this.historyVisible = !this.historyVisible;
    },
    minimize() {
      if (this.$electron) {
        let window = this.$electron.remote.getCurrentWindow();
        window.minimize();
      }
    },
    maximizeOrRestore() {
      if (this.$electron) {
      let window = this.$electron.remote.getCurrentWindow();
      if (this.isMaximized) {
          window.restore();
      } else {
          window.maximize();
      }
          this.isMaximized = !this.isMaximized;
      }
    },
    close() {
      if (this.$electron) {
          let window = this.$electron.remote.getCurrentWindow();
          window.close();
      }
    },
    clearHistory() {
          this.$emit('clear-history');
    },
  },
};
</script>