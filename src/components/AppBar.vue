<template>
    <div class="h-1">
      <!-- This div is for resizing control -->
    </div>
    <div class="flex" style="-webkit-app-region: drag;">
      <div class="flex" style="-webkit-app-region: no-drag;">
        <button>
          <MenuSvg class="w-10 h-10" />
        </button>
        <div class="flex justify-end space-x-4 mr-4">
          <button class="text-gray-500 hover:text-gray-700 focus:outline-none" @click="minimize">
            <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 12H4"></path>
            </svg>
          </button>
  
          <button class="text-gray-500 hover:text-gray-700 focus:outline-none" @click="maximizeOrRestore">
            <svg v-if="!isMaximized" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 6h12v12H6z"></path>
            </svg>
            <svg v-else class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 4h16v16H4z"></path>
            </svg>
          </button>
  
          <button class="text-gray-500 hover:text-gray-700 focus:outline-none" @click="close">
            <svg class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>
      </div>
    </div>
  </template>


<script>
import MenuSvg from '@/components/svg/MenuSvg.vue';

export default {
    name: 'AppBar',
    components: {
      MenuSvg
    },
    methods: {
    }
}
</script>