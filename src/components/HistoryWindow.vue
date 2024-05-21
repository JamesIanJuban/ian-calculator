<template>
  <transition name="slide-fade">
    <div v-if="show" 
      class="fixed top-0 left-0 w-full h-full flex justify-center items-center z-50 bg-black bg-opacity-50">
    <div class="bg-white rounded-lg p-8 max-w-lg w-60 text-gray-700 relative">
    <h3 class="text-lg font-semibold mb-4">History</h3>
    <ul class="divide-y divide-gray-300">
    <li v-if="history.length === 0" 
      class="py-2 text-gray-700">No history yet</li>
    <!-- Ensure correct rendering of calculation history -->
    <li v-else v-for="(calculation, index) in history.slice().reverse()" 
      :key="index" 
      class="py-2">
    <div class="flex justify-between items-center">
    <span class="text-gray-700">{{ calculation.expression }}</span>
    <span class="text-green-500">{{ calculation.result }}</span>
    </div>
    </li>
    </ul>
    <!-- Add clear history button -->
    <button @click="clearHistory" 
      class="mt-4 bg-red-500 hover:bg-red-600 text-white font-semibold px-4 py-2 rounded-lg focus:outline-none">
          Clear History
    </button>
        <!-- Add close button -->
    <button @click="toggle" 
      class="absolute top-0 right-0 m-3 text-white hover:text-gray-900 focus:outline-none">
    <svg xmlns="http://www.w3.org/2000/svg" 
      class="h-7 w-8 bg-red-500  rounded-lg" 
      fill="none" 
      viewBox="0 0 24 24" 
      stroke="currentColor">
    <path stroke-linecap="round" 
      stroke-linejoin="round" 
      stroke-width="2" 
      d="M6 18L18 6M6 6l12 12" />
    </svg>
    </button>
    </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'HistoryWindow',
  props: {
    show: Boolean,
    history: {
      type: Array,
      required: true
    }
  },
  methods: {
    toggle() {
      // Emit toggle event to hide the history window
      this.$emit('toggle');
    },
    clearHistory() {
      // Emit clear-history event to clear the history
      this.$emit('clear-history');
    }
  }
};
</script>