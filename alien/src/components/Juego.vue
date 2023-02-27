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
                let obstaculo = document.createElement('div');

                let aleat = Math.floor(Math.random() * 470);
                obstaculo.style.top = aleat + 'px';
                obstaculo.id = 'obstaculo';

                let tipo =  Math.floor(Math.random() * 3);
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
                    if(obstaculo.getBoundingClientRect().left < 329 && obstaculo.getBoundingClientRect().right > 229) {
                        let choque = (this.verticalPosition + 100) < aleat || this.verticalPosition > (aleat + parseInt(altoObstaculo.substring(0, altoObstaculo.length - 2)));
                        if(!choque) {
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
            // setTimeout(() => {
            //     document.getElementById('alien').className = '';
            // }, 800);
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
    min-width: 65px;
    min-height: 65px;
    position: absolute;
    left: 33cm;
    overflow-x: hidden;
    animation: moveObstaculo 2s linear;
    background-repeat: no-repeat;
    background-size: cover;
}

@keyframes moveObstaculo {
    100% {
        left: -3cm;
        display: none;
    }
}
</style>
