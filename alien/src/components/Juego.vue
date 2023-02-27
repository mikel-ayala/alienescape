<template>
    <div>
        <img src="../assets/ufo.gif" id="alien" />
        <audio id="GameOver">
            <source src="../assets/game-over.mp3" type="audio/mpeg" />
        </audio>
        <audio id="PlaySound">
            <source src="../assets/play.mp3" type="audio/mpeg" />
        </audio>
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
            this.moverse(val);
        },
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
            this.playSound();
            let obstaculo = document.createElement('div');

            let aleat = Math.floor(Math.random() * 470);
            obstaculo.style.top = aleat + 'px';
            obstaculo.id = 'obstaculo';
            document.getElementById('juego').appendChild(obstaculo);

            let hit = setInterval(() => {
                if (obstaculo.getBoundingClientRect().left < 329 && obstaculo.getBoundingClientRect().right > 229) {
                    let choque = (this.verticalPosition + 100) < aleat || this.verticalPosition > (aleat + 65);
                    if (!choque) {
                        let choqueSound = document.getElementById("GameOver");
                        choqueSound.volume = 1;
                        choqueSound.play();
                        alert('Choque');
                    }
                }
            }, 10);

            setTimeout(() => {
                obstaculo.remove();
                clearInterval(hit);
            }, 2000);

            setTimeout(() => {
                this.randomObjects();
            }, (Math.floor(Math.random() * 2000)) + 1000);
        },
        moverse(direccion) {
            if (this.estado == "subir") {
                this.subir();
            } else if (this.estado == "bajar") {
                this.bajar();
            }
            if (this.estado != "quieto") {
                if (this.estado == direccion) {
                    setTimeout(() => {
                        this.moverse(direccion);
                    }, 15);
                }
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
        },
        playSound() {
            let choqueSound = document.getElementById("PlaySound");
            choqueSound.volume = 1;
            choqueSound.play();
        },
    },
    mounted() {
        window.addEventListener('keydown', (e) => { this.changeState(e) });
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
    height: 100px;
    width: 100px;
    position: relative;
    top: 6cm;
    left: 2cm;
}

#obstaculo {
    height: 65px;
    width: 65px;
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
