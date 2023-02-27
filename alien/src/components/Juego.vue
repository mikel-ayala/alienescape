<template>
    <div>
        <h3 id="puntos">{{ puntos }}</h3>
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
            puntos: 0,
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

            let tipo = Math.floor(Math.random() * 3);
            let altoObstaculo;
            let largoObstaculo;

            switch (tipo) {
                case 0:
                    altoObstaculo = '120px';
                    largoObstaculo = '120px';
                    obstaculo.style.backgroundImage = "url('./src/assets/helicoptero.gif')";
                    break;
                case 1:
                    altoObstaculo = '80px';
                    largoObstaculo = '200px';
                    obstaculo.style.backgroundImage = "url('./src/assets/helicopter2.png')";
                    break;
                case 2:
                    altoObstaculo = '120px';
                    largoObstaculo = '200px';
                    obstaculo.style.backgroundImage = "url('./src/assets/helicopter3.gif')";
                    break;
            }

            obstaculo.style.height = altoObstaculo;
            obstaculo.style.width = largoObstaculo;

            document.getElementById('juego').appendChild(obstaculo);

            let hit = setInterval(() => {
                if (obstaculo.getBoundingClientRect().left < 329 && obstaculo.getBoundingClientRect().right > 229) {
                    let choque = (this.verticalPosition + 100) < aleat || this.verticalPosition > (aleat + parseInt(altoObstaculo.substring(0, altoObstaculo.length - 2)));
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
        puntuacion() {
            this.puntos++;

            if(this.puntos%1000 == 0) {
                let puntosCartel = this.puntos/1000 + ' KM';
                let divCartel = document.createElement('div');
                let cartel = document.createElement('img');
                let h3Cartel = document.createElement('h3');

                divCartel.id = 'divCartel';

                h3Cartel.innerHTML = puntosCartel;
                divCartel.appendChild(h3Cartel);

                cartel.id = 'cartel';
                cartel.setAttribute('src', '/src/assets/cartelKilometros.png');
                divCartel.appendChild(cartel);

                document.getElementById('juego').appendChild(divCartel);

                setTimeout(() => {
                    divCartel.remove();
                }, 4000);
            }
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
            if (this.verticalPosition > 0) {
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

        setInterval(this.puntuacion, 20);
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
    height: 80px;
    width: 80px;
    position: relative;
    top: 6cm;
    left: 2cm;
    border-radius: 100px 100px 0px 0px;
    border: solid red 1px;
}

#alien img {
    height: 120%;
    width: 120%;
    position: absolute;
    right: -8px;
    top: -5px;
}

#obstaculo {
    min-width: 65px;
    min-height: 65px;
    position: absolute;
    left: 33cm;
    overflow-x: hidden;

    animation: moveObstaculo 2s linear;
    background-repeat: no-repeat;
    background-size: cover;
}

#divCartel {
    position: absolute;
    top: 85%;
    left: 33cm;
    opacity:0.9;

    animation: moveObstaculo 4s linear;
}

#divCartel h3 {
    position: absolute;
    top:27px;
    left: 29px;
    font-family: nasalization;
}

#divCartel img {
    height: 100px;
    width: 100px;
}

#puntos {
    text-align: end;
    margin-right: 20px;
}

@keyframes moveObstaculo {
    100% {
        left: -3cm;
        display: none;
    }
}
</style>
