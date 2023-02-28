<template>
    <div>
        <h1 id="perdido">Has perdido</h1>
        <img src="../assets/ufo2.png" id="ufo" />
        <img src="../assets/fuego.gif" id="fuego">
        <div id="abajo">
            <h2>Puntuacion: <span id="puntosfin">{{ puntuacion }}</span></h2>
            <br>
            <button @click="reload"><b> JUGAR</b></button>
        </div>

    </div>
</template>

<script>
export default {

    data() {
        return {
            puntuacion: ""
        }
    },
    mounted() {
        setInterval(this.actualizarPuntos, 20);
    },
    methods: {
        actualizarPuntos() {
            this.puntuacion = sessionStorage.puntos;
        },
        reload(){
            window.location.reload();
        }
    }
}
</script>
<style>
@font-face {
    font-family: nasalization;
    src: url('./assets/nasalization-rg.otf');
}

#perdido {
    color: white;
    font-family: nasalization;
    text-align: center;
    margin-top: 5vh;
}

#ufo {
    z-index: 1;
    width: 90px;
    transform: rotate(-85deg);
    position: absolute;
    left: 16vw;
    top: 15vh;
}

#fuego {
    z-index: 2;
    position: absolute;
    margin-left: 15vw;

}

h2 {
    color: white;
}
#puntosfin{
    color: goldenrod;
}


button{
    padding: 15px 20px;
    border-radius: 10px;
    background-color: rgb(38, 206, 38);
    color: white;
    font-family: nasalization;
}

#abajo{
    text-align: center;
    font-family: nasalization;
    margin-top: 12vw;
}
</style>