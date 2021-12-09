<template>
  <div class="bg">
    <Calculate/>
    <footer>© Saïda Benaïssa 2021</footer>
  </div>
</template>

<script>
import Calculate from './components/Calculate';
export default {
  components: {
    Calculate
  }
}
</script>
<style >
  .bg {
    background-color: #231F20;;
    width: 100vw;
    height: 100vh;
    padding: 2rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  html, body {
    font-family: 'Sora', sans-serif;
  }
  footer{
    color: white;
  }
</style>