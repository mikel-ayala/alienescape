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
  <img id="corriendo" src="./assets/alien.gif" alt="">
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
    color: white;
  }
  main {
    position: relative;
    width: 100vw;
    height: 100vh;
    background-color: #121212;
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
    background-image:url('assets/Desert.gif');
    background-repeat:no-repeat;
    background-size: cover;
    overflow: hidden;
  }
  #corriendo {
    position: absolute;
    top: 90vh;
    left: -5vw;
    z-index: 3;
    width: auto;
    height: 10vh;  
    animation: corriendo 5s;
  }

  @keyframes inicio {
    from {
      transform: translateY(-800px);
    }
    to {
      transform: translateY(0px);

    }
  }

  @keyframes corriendo {
    from {
      transform: translateX(0);
    }
    to {
      transform: translateX(1535px);
      display: none;
    }
  }
</style>
