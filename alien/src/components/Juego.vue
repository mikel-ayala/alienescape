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
        window.addEventListener('keydown', this.jump);
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


@keyframes jump {
    0% {
        padding-bottom: 0;
    }

    5% {
        transform: scale(1.1, 0.95);
    }

    50% {
        transform: translateY(-200px);
    }

    95% {}

    100% {
        padding-bottom: 0;
    }
}

@keyframes down {
    0% {
        padding-bottom: 0;
    }

    5% {
        transform: scale(1.1, 0.95);
    }

    50% {
        transform: translateY(+200px);
    }

    95% {}

    100% {
        padding-bottom: 0;
    }
}
</style>