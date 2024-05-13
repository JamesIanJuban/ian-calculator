<template>
  <article class="text-center overflow-hidden min-h-screen"> 
    <AppBar />
    <h1 class="text-4xl text-white bg-gradient-to-br from-gray-800 to-gray-900 mt-6 font-bold">Scientific Calculator</h1>
    <CalculatorContainer/>
  </article>
</template>
  
<script>
import AppBar from './components/AppBar.vue';
import CalculatorContainer from './components/CalculatorContainer.vue';

export default {
    name: 'App',
    components: {
      AppBar,
      CalculatorContainer,
  }
}
</script>