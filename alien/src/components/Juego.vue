<template>
    <div>
        <img src="../assets/ufo.gif" id="alien">  
    </div>
</template>

<script>
    export default {
        data() {
            return {

            }
        }, 
        methods: {
            jump() {
                console.log(document.getElementById('alien').classList.value);

                if(!document.getElementById('alien').classList.contains('jump'))
                    document.getElementById('alien').className = 'jump';
                

                setTimeout(() => {
                    document.getElementById('alien').className = '';
                }, 800);
            },
            randomObjects() {
                setTimeout(() => {
                    let randNum = Math.floor(Math.random() * 2);
                    if(randNum == 0) {
                        
                    } else if(randNum == 1) {

                    } else {

                    }
                }, 1000);
            }
        },
        mounted() {
            window.addEventListener('keypress', this.jump);
        }
    }
</script>

<style>
    img {
        width: 30%;
    }

    .jump {
        animation: jump 0.8s;
        animation-timing-function: cubic-bezier(.41,.54,.4,1.02); 
    }

    #alien{
        margin-top: 20%;
        margin-left: 2cm;
        height: 3cm;
        width: 3cm;
    }
    

    @keyframes jump {
        0% {
            padding-bottom: 0;
        }

        5% {
            transform: scale(1.1, 0.95);
        }

        50% {
            transform: translateY(-100px);
        }

        95% {
        }

        100% {
            padding-bottom: 0;
        }
    }
</style>