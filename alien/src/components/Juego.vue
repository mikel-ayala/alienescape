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
        }
    },
    methods: {
        jump(e) {

            if (e.keyCode == '38') {
                if (this.verticalPosition > 10) {
                    this.verticalPosition = this.verticalPosition - 10;
                    //console.log(this.verticalPosition);
                    document.getElementById('alien').style.top = this.verticalPosition + "px";
                }
            } else if (e.keyCode == '40') {
                if (this.verticalPosition < 470) {
                    this.verticalPosition = this.verticalPosition + 10;
                    //console.log(this.verticalPosition);
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

                //console.log(aleat);

                obstaculo.id = 'obstaculo';
                document.getElementById('juego').appendChild(obstaculo);
                
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
    },
    mounted() {
        window.addEventListener('keydown', this.jump);
        setTimeout(() => {
            setInterval(this.randomObjects, 3000);
            //this.randomObjects();
        }, 2000);
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