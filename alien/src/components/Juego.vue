<template>
  <div>
    <img src="../assets/ufo.gif" id="alien" />
  </div>
</template>

<script>
export default {
    data() {
        return {
            verticalPosition: 230,
            estado: "quieto",
            moviendo: true,
            aliens: []
            
        }
    },
    watch: {
        // watching top-level property
        estado(val, oldVal) {
            this.moverse();
        },

        aliens(val, oldVal){
            // si hay this.aliens
            // val[0] 
            // alien.left <= ovni righ
            //     compruebo si se choca
            //     alien right = alien.lefg + algo
        }
    }
    ,
    methods: {
        changeState(e) {
            if (e.keyCode == '38') {
                this.estado = 'subir';
            } else if (e.keyCode == '40') {
                this.estado = "bajar";
            }
        },
        randomObjects() {
                let obstaculo = document.createElement('div');
                let alien = document.getElementById('alien');

                let aleat = (Math.floor(Math.random() * 470)) - 100;
                obstaculo.style.top = aleat + 'px';
                obstaculo.id = 'obstaculo';
                document.getElementById('juego').appendChild(obstaculo);

                setTimeout(() => {
                    obstaculo.remove();
                    clearInterval(hit);
                }, 2000);

                setTimeout(() => {
                    this.randomObjects();
                }, (Math.floor(Math.random() * 2000)) + 1000);
            },
        moverse() {
            if (this.estado == "subir") {
                this.subir();
            } else if (this.estado == "bajar") {
                this.bajar();
            }
            if (this.estado != "quieto") {

                setTimeout(() => {
                    this.moverse();
                }, 15);
            }
        },
        subir() {
            if (this.verticalPosition > 10) {
                this.verticalPosition = this.verticalPosition - 10;
                document.getElementById('alien').style.top = this.verticalPosition + "px";
            }
        },
        bajar(e) {
            if (this.verticalPosition < 470) {
                this.verticalPosition = this.verticalPosition + 10;
                document.getElementById('alien').style.top = this.verticalPosition + "px";
            }
            // setTimeout(() => {
            //     document.getElementById('alien').className = '';
            // }, 800);
        },
    },
    mounted() {
        window.addEventListener('keydown', (e) => { this.changeState(e)});
        window.addEventListener('keyup', () => {
            this.estado = "quieto";
        });

        setTimeout(() => {
            this.randomObjects();
        }, 2000);
    }
}
</script>

<style>
img {
    width: 30%;
}

.jump {
    animation: jump 1s;
    animation-timing-function: cubic-bezier(0.41, 0.54, 0.4, 1.02);
}

.down {
    animation: down 1s;
    animation-timing-function: cubic-bezier(0.41, 0.54, 0.4, 1.02);
}

#alien {
    height: 3cm;
    width: 3cm;
    position: relative;
    top: 6cm;
    left: 2cm;
}

#obstaculo {
    height: 2cm;
    width: 2cm;
    position: absolute;
    left: 33cm;
    background-color: black;
    overflow-x: hidden;
    animation: moveObstaculo 2s linear;
}
@keyframes moveObstaculo {
    100% {
        left: -3cm;
        display: none;
    }
}

</style>
