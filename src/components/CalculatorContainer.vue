<template>
  <div class="overflow-hidden justify-center items-center p-8 relative bg-gradient-to-br from-gray-800 to-gray-900">
    <div class="display mb-6 mt-6 flex justify-center">
      <input
        type="text"
        v-model="inputStr"
        placeholder="0"
        autofocus
        @keydown.enter="calculate"
        @input="validateInput"
        class="input-text w-full h-[15rem] max-w-xl px-8 py-6 md:py-8 text-2xl md:text-3xl rounded-lg text-white border-2 border-red-500/50 bg-red-600 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 placeholder-gray-100 focus:border-red-500 focus:outline-none transition duration-300 ease-in-out"
      />
    </div>
    <div class="grid grid-cols-5 gap-4 px-6 py-4">
      <button
        v-for="item in numeric"
        :key="item.text"
        class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg px-6 py-3 text-center mr-1 mb-2"
        @click="handleButtonClick(item)"
      >
        {{ item.text }}
      </button>
      <button
        class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-6 py-2.5 text-center mr-1 mb-2"
        @click="remove"
      >
        ←
      </button>
      <button
        class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-6 py-2.5 text-center mr-1 mb-2"
        @click="clear"
      >
        AC
      </button>
      <button
        class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-6 py-2.5 text-center mr-1 mb-2"
        @click="calculate"
      >
        =
      </button>
    </div>
    <transition name="slide">
      <div v-if="showHistory" class="history-container fixed right-0 top-0 h-screen w-1/2 bg-gray-900 shadow-lg overflow-y-auto z-50">
        <button @click="toggleHistory" class="close-button absolute top-4 right-4 bg-red-500 text-white font-bold rounded-full h-8 w-8 flex items-center justify-center focus:outline-none">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
          </svg>
        </button>
        <AppBar :historyData="history" />
        <ul class="divide-y divide-gray-300">
          <li v-for="(calculation, index) in history.slice().reverse()" :key="index" class="py-2">
            <div class="flex justify-between items-center">
              <span>{{ calculation.expression }} = {{ calculation.result }}</span>
            </div>
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>

<script>
import { numeric } from '@/data.js';

export default {
  name: 'CalculatorContainer',
  data() {
    return {
      inputStr: '',
      numeric: numeric,
      history: [],
      showHistory: false,
    };
  },
  methods: {
    handleButtonClick(button) {
      if (button.operation) {
        this.inputStr += button.operation;
      } else {
        this.inputStr += button.text;
      }
    },
    validateInput(event) {
      if (event.key === ' ') {
        this.addSpace();
      } else {
        this.inputStr = this.inputStr.replace(/[^-()\d/*+.π ]/g, '');
      }
    },
    clear() {
      this.inputStr = '';
    },
    remove() {
      this.inputStr = this.inputStr.slice(0, -1);
    },
    calculate() {
      try {
        if (!this.inputStr.trim()) {
          this.inputStr = '';
          return;
        }
        let expression = this.inputStr.replace(/%/g, '/100');
        const result = eval(expression);
        if (!isNaN(result) && result !== Infinity) {
          this.inputStr = result.toString();
          this.history.push({
            expression: expression,
            result: result.toString(),
            timestamp: new Date().toLocaleString(),
          });
          this.$emit('update-history', this.history);
        } else {
          throw new Error('Invalid expression');
        }
      } catch (error) {
        this.inputStr = error.message;
      }
    },
    toggleHistory() {
      this.showHistory = !this.showHistory;
    },
    clearHistory() {
      this.history = [];
    },
  },
};
</script>