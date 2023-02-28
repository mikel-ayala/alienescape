<script>
  import Juego from './components/Juego.vue';
  import Lose from './components/lose.vue';

  export default {
    components: {
      Juego,
      Lose
    }
  }
</script>
<template>
  <h1 id="titulo">ALIEN ESCAPE</h1>  
  <img id="corriendo" src="./assets/alien.gif" alt="">
  <Lose id="lose"/>
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
    overflow: hidden;
  }
  #titulo {
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
  #lose{
    position: absolute;
    left: 30vw;
    top: 25vh;
    background-color: #121212;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
    z-index: 4;
    width: 40vw;
    height: 50vh;
    border-radius: 25px;
    display: none;
  }

  .showpuntos{
    animation: puntos 2s;
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

  @keyframes puntos{
    from{
      transform: translateY(800px);
      display: block;
    }
    to{
      transform: translateY(0);
      display: block;
    }
  }

</style>
