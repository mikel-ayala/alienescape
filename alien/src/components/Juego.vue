<template>
    <div>
        <img src="../assets/ufo.gif" id="alien">
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
                this.estado = "subir";
            } else if (e.keyCode == '40') {
                this.estado = "bajar";
            }
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
        randomObjects() {
            setTimeout(() => {
                let randNum = Math.floor(Math.random() * 2);
                if (randNum == 0) {

                } else if (randNum == 1) {

                } else {

                }
            }, 1000);
        }
    },
    mounted() {
        window.addEventListener('keydown', (e) => { this.changeState(e)});
        window.addEventListener('keyup', () => {
            this.estado = "quieto";
        });
    }
}
</script>

<style>
img {
    width: 30%;
}

.jump {
    animation: jump 1s;
    animation-timing-function: cubic-bezier(.41, .54, .4, 1.02);
}

.down {
    animation: down 1s;
    animation-timing-function: cubic-bezier(.41, .54, .4, 1.02);
}

#alien {
    height: 3cm;
    width: 3cm;
    position: relative;
    top: 6cm;
    left: 2cm;
}
</style>