<template>
  <article class="text-center"> 
    <h1 class="text-4xl text-red-500 mt-10 mb-6 font-bold">Scientific Calculator</h1>
      <CalculatorContainer/>
  </article>
</template>
  
<script>
import CalculatorContainer from './components/CalculatorContainer.vue'

export default {
    name: 'App',
    components: {
    CalculatorContainer
  }
}
</script>