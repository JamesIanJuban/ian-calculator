<template>
    <div class="container box justify-center items-center p-8">
        <!-- Calculator display -->
        <div class="display mb-12 mt-12 flex justify-center">
          <input type="text" v-model="inputStr" placeholder="Enter Expression" @keydown.enter="calculate" @input="validateInput" class="input-text w-full max-w-xl px-6 py-4 md:py-6 text-lg rounded-lg text-white border-2 border-gray-300 bg-blue-900 placeholder-gray-300 focus:border-blue-500 focus:outline-none transition duration-300 ease-in-out">
        </div>
        <!-- Operation buttons -->  
        <div class="grid grid-cols-5 gap-5 px-6 py-4">
            <button v-for="item in numeric" :key="item.text" class="text-red-500 py-1.5 bg-gray-200 hover:bg-gray-300" @click="handleButtonClick(item)">{{ item.text }}</button>
            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="calculate">=</button>
            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="clear">AC</button>
            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="remove">←</button>
        </div>
    </div>
</template>
  
<script>
import { numeric } from '@/data.js';
  
export default {
            name: "CalculatorContainer",
      data() {
          return {
            inputStr: '',
            numeric: numeric
          };
      },
  methods: {
      handleButtonClick(button) {
          if (button.operation) {
            this.inputStr += button.operation;
          } 
          else {
            this.inputStr += button.text;
          }
      },
      validateInput() {
            this.inputStr = this.inputStr.replace(/[^-()\d/*+.π]|%/g, '');
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
          const result = Function('"use strict";return (' + expression + ')')();
          if (!isNaN(result) && result !== Infinity) {
            this.inputStr = result.toString();
          } else {
            throw new Error('Invalid expression');
          }
          } 
          catch (error) {
            this.inputStr = error.message;
          }
      }
  }
};
</script>
  
  