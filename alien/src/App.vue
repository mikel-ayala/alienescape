<script>
  import Juego from './components/Juego.vue';

  export default {
    components: {
      Juego
    }
  }
</script>

<template>
  <h1>ALIEN ESCAPE</h1>
  <main>
    <Juego  id="juego"/>
  </main>
</template>

<style>
@font-face {
  font-family: nasalization;
  src: url('./assets/nasalization-rg.otf');
}
  * {
    margin: 0;
    padding: 0;
  }
  h1 {
    position: absolute;
    width: 80vw;
    height: 20vh;
    left: 10vw;
    top: 40vh;
    text-align: center;
    vertical-align: middle;
    font-family: nasalization;
    font-size: 8em;
    z-index: 1;
  }
  main {
    position: relative;
    width: 100vw;
    height: 100vh;
  }
  #juego {
    position: absolute;
    width: 80vw;
    height: 80vh;
    top: 10vh;
    left: 10vw;
    border-radius: 25px;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    animation: inicio 3s;
    z-index: 2;
  }

  @keyframes inicio {
    from {
      transform: translateY(-800px);
    }
    to {
      transform: translateY(0px);

    }
  }
</style>
