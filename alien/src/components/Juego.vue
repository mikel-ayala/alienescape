<template>
    <div>
        <img src="../assets/ufo.gif" id="alien">
    </div>
</template>

<script>
export default {
    data() {
        return {
            verticalPosition: 230
        }
    },
    methods: {
        jump(e) {

            // console.log(e.keyCode);
            // console.log(document.getElementById('alien').classList.value);

            if (e.keyCode == '38') {
                if (this.verticalPosition > 10) {
                    this.verticalPosition = this.verticalPosition - 10;
                    console.log(this.verticalPosition);
                    document.getElementById('alien').style.top = this.verticalPosition + "px";
                }
                // if (!document.getElementById('alien').classList.contains('jump'))
                //     document.getElementById('alien').className = 'jump';
                // document.getElementById('alien').style.transla = '5px';
            } else if (e.keyCode == '40') {
                if (this.verticalPosition < 470) {
                    this.verticalPosition = this.verticalPosition + 10;
                    console.log(this.verticalPosition);
                    document.getElementById('alien').style.top = this.verticalPosition + "px";
                }
                // if (!document.getElementById('alien').classList.contains('down'))
                //     document.getElementById('alien').className = 'down';
            }

            setTimeout(() => {
                document.getElementById('alien').className = '';
            }, 800);
        },
        randomObjects() {
                let obstaculo = document.createElement('div');

                let aleat = (Math.floor(Math.random() * 470)) - 100;
                obstaculo.style.top = aleat + 'px';

                console.log(aleat);

                
                obstaculo.id = 'obstaculo';
                document.getElementById('juego').appendChild(obstaculo);
        },
    },
    mounted() {
        window.addEventListener('keydown', this.jump);
        setTimeout(() => {
            //setInterval(this.randomObjects, 3000);
            this.randomObjects();
        }, 3000);
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

#obstaculo {
    height: 2cm;
    width: 2cm;
    position: relative;
    left: 33cm;
    background-color: black;

    animation: moveObstaculo 2s linear;
}


@keyframes moveObstaculo {

    100% {
        left: 0cm;
        display: none;
    }
}

</style>