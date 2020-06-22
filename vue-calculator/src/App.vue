<template>
  <div id="app">
    <Calculator></Calculator>
  </div>
</template>

<script>
import calculator from './components/Calculator.vue';
export default {
  name: 'app',
  components:{
    Calculator: calculator,
  },
  data () {
    return {

    }
  }
}
</script>

<style scoped>

#app{
  width: 100%;
  height: 861px;
  padding-top: 50px;
  background: url("./assets/numbers.png") rgba(255, 220, 226, 0.849);
  background-size: 100% 80%;  
  background-position: bottom;
  background-repeat: no-repeat;

}

</style>>

</style>
