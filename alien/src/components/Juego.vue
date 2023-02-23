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
        }
    },
    watch: {
        // watching top-level property
        estado(val, oldVal) {
          this.moverse();
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

                let aleat = (Math.floor(Math.random() * 470)) - 100;
                obstaculo.style.top = aleat + 'px';
                obstaculo.id = 'obstaculo';
                document.getElementById('juego').appendChild(obstaculo);

                //console.log(aleat);
                let hit = setInterval(() => {
                    console.log('Y Obs:' + obstaculo.getBoundingClientRect().y + ' Bottom Obs: ' + obstaculo.getBoundingClientRect().bottom);
                    console.log('Y Alien:' + document.getElementById('alien').getBoundingClientRect().y + ' Alien Obs: ' + document.getElementById('alien').getBoundingClientRect().bottom);
                    if(document.getElementById('alien').getBoundingClientRect().y >= obstaculo.getBoundingClientRect().y
                        && document.getElementById('alien').getBoundingClientRect().y <= obstaculo.getBoundingClientRect().bottom
                        && document.getElementById('alien').getBoundingClientRect().x >= obstaculo.getBoundingClientRect().x
                        && document.getElementById('alien').getBoundingClientRect().x <= obstaculo.getBoundingClientRect().right
                            || document.getElementById('alien').getBoundingClientRect().y >= obstaculo.getBoundingClientRect().y
                            && document.getElementById('alien').getBoundingClientRect().y <= obstaculo.getBoundingClientRect().bottom
                            && document.getElementById('alien').getBoundingClientRect().right >= obstaculo.getBoundingClientRect().x
                            && document.getElementById('alien').getBoundingClientRect().right <= obstaculo.getBoundingClientRect().right
                                || document.getElementById('alien').getBoundingClientRect().bottom >= obstaculo.getBoundingClientRect().y
                                && document.getElementById('alien').getBoundingClientRect().bottom <= obstaculo.getBoundingClientRect().bottom
                                && document.getElementById('alien').getBoundingClientRect().x >= obstaculo.getBoundingClientRect().x
                                && document.getElementById('alien').getBoundingClientRect().x <= obstaculo.getBoundingClientRect().right
                                    || document.getElementById('alien').getBoundingClientRect().bottom >= obstaculo.getBoundingClientRect().y
                                    && document.getElementById('alien').getBoundingClientRect().bottom <= obstaculo.getBoundingClientRect().bottom
                                    && document.getElementById('alien').getBoundingClientRect().right >= obstaculo.getBoundingClientRect().x
                                    && document.getElementById('alien').getBoundingClientRect().right <= obstaculo.getBoundingClientRect().right) {
                            alert('Chocaste');
                        }
                    }, 100);

                setTimeout(() => {
                    obstaculo.remove()
                    clearInterval(hit);
                }, 2000);
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
            setInterval(this.randomObjects, 2500);
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
    position: relative;
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
