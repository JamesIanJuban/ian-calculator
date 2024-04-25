<template>
  <article class="text-center"> 
    <h1 class="text-4xl font-bold">Scientific Calculator</h1>
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