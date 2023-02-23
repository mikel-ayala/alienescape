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

            if (e.keyCode == '38') {
                if (this.verticalPosition > 10) {
                    this.verticalPosition = this.verticalPosition - 10;
                    console.log(this.verticalPosition);
                    document.getElementById('alien').style.top = this.verticalPosition + "px";
                }
            } else if (e.keyCode == '40') {
                if (this.verticalPosition < 470) {
                    this.verticalPosition = this.verticalPosition + 10;
                    console.log(this.verticalPosition);
                    document.getElementById('alien').style.top = this.verticalPosition + "px";
                }
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

                setTimeout(() => {
                    obstaculo.remove()
                }, 2000);
        },
    },
    mounted() {
        window.addEventListener('keydown', this.jump);
        setTimeout(() => {
            setInterval(this.randomObjects, 3000);
            //this.randomObjects();
        }, 1500);
    }
}
</script>

<style>
img {
    width: 30%;
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