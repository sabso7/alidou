<template>
<div>
    <svg viewBox="0 0 1200 800" height="800" width="800" xmlns="http://www.w3.org/2000/svg" version="1.1">
        <g transform-origin="center" transform="scale(1, 1) rotate(0)">
        <rect x="0" y="0" width="800" height="600" fill="#010510ff">
        </rect>
        <linearGradient id="linear-gradient-r1">
            <stop offset="0%" stop-color="#d54401ff" stop-opacity="100%"></stop>
            <stop offset="100%" stop-color="#f80242ff" stop-opacity="100%"></stop>
        </linearGradient>
        <filter x="-5%" y="-5%" width="110%" height="110%" filterUnits="objectBoundingBox" id="strokeStyle">
            <feTurbulence type="fractalNoise" :baseFrequency="freq" numOctaves="5" result="f1" stitchTiles="stitch"></feTurbulence>
            <feColorMatrix type="matrix" values="0 0 0 0 0, 0 0 0 0 0, 0 0 0 0 0, 0 0 0 -1.5 1.5" result="f2">
            </feColorMatrix>
            <feComposite operator="in" in2="f2b" in="SourceGraphic" result="f3"></feComposite>
            <feTurbulence type="fractalNoise" baseFrequency="0" numOctaves="9" result="noise"></feTurbulence>
            <feDisplacementMap xChannelSelector="R" yChannelSelector="G" scale="8" in="f3" result="f4"></feDisplacementMap>
        </filter>
            <g filter="url(#strokeStyle)">
                <path d="M10 350 l 150 -300" fill="#d54401ff"/>
                <path d="M125,85 a60,60 0 1,0 -115,0" fill="#d54401ff" />
                <path d="M10,85 a60,60 0 0,0 115,0" fill="#d54401ff" />
                <path d="M 60 190 103.12167118117213 100.43665465293451 l69.40938873464862 -86.91741500934585 l68.58663798123598 127.8204105393961 l80.51999023060003 -69.87274225987494 l66.8001281072696 125.07974198274313 l57.17713452254732 -105.68280499381943 l27.02001218497753 64.05342778377235 l35.50264996414383 -138.93343471409753 l90.99209652841091 180.88560262881218" fill="none" stroke-linecap="round" stroke="url(#linear-gradient-r1)" stroke-width="5" style="transform-origin: center center 0px; transform: scale(1.1) translate(40px, 180px); transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1) 0s;"></path>
                <!--<path d="M 86 354 l63.12167118117213 119.43665465293451 l69.40938873464862 -86.91741500934585 l68.58663798123598 127.8204105393961 l80.51999023060003 -69.87274225987494 l66.8001281072696 125.07974198274313 l57.17713452254732 -105.68280499381943 l27.02001218497753 64.05342778377235 l35.50264996414383 -138.93343471409753 l37.99209652841091 80.88560262881218" fill="none" stroke-linecap="round" stroke-linejoin="miter" filter="url(#shadow-r5)" stroke="url(#linear-gradient-r1)" stroke-width="18" style="transform-origin: center center 0px; transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1) 0s;"></path>-->              
                <path :d="'M '+ mov1 +' '+ mov2 +' C'+ curves[0] +' '+ curves[1] +' '+ curves[2] +' '+ curves[3] +' '+ curves[4] +' '+ curves[5]" fill="none" stroke-linecap="round" stroke="url(#linear-gradient-r1)" stroke-width="5.5" style="transform-origin: center center 0px; transform: scale(1) translate(0px, 480px); transition: transform 5ms ease-in-out;"></path>
                <path :d="'M '+ mov3 +' '+ mov4 +' C'+ curves[0] +' '+ curves[1] +' '+ curves[2] +' '+ curves[3] +' '+ curves[4] +' '+ curves[5]" fill="none" stroke-linecap="round" stroke="url(#linear-gradient-r1)" stroke-width="8.5" style="transform-origin: center center 0px; transform: scale(1.8) translate(0px, 380px); transition: transform 6ms ease-in-out;"></path>
                <path :d="'M '+ mov5 +' '+ mov6 +' C'+ curves[0] +' '+ curves[1] +' '+ curves[2] +' '+ curves[3] +' '+ curves[4] +' '+ curves[5]" fill="none" stroke-linecap="round" stroke="url(#linear-gradient-r1)" stroke-width="10.5" style="transform-origin: center center 0px; transform: scale(0.8) translate(0px, 450px); transition: transform 9ms ease-in-out;"></path>
            </g>
        </g>
    </svg>
    </div>
</template>
<script>
    export default {
        data() {
            return{
                mov1: 800,
                mov2: 5,
                mov3: 1500,
                mov4: -10,
                mov5: 1500,
                mov6: 60,
                curves: [900,0,800,0,-500,0],
                stop: true,
                interval: 200,
                freq: 0.5
            }
        },
        created () {
            if (process.client) { 
            window.addEventListener('scroll', this.checkScroll);
            }
        },
        destroy() {
            window.removeEventListener('scroll');
        },
        mounted: function() {
            //this.start();
        },
        methods:{
            checkScroll() {
                /*if(this.stop == true && window.scrollY < 669){
                    this.start();
                }*/
            },
            start() {
                let count = 0;
                let topDown = true;
                this.curves = [800,0,300,0,-500,0];
                let boucle = setInterval(() => {
                    if(this.freq > 0.8){
                        topDown = true;
                    }
                    if(this.freq < 0.5 ){
                        topDown = false;
                    }
                    if(topDown){
                        this.freq -= 0.1
                    }else{
                        this.freq += 0.1
                    }
                    if(window.scrollY === 669){
                        clearInterval(boucle);
                        this.stop = true;
                        this.count = 0;
                        this.interval = 100;
                    }
                    let index = count % this.curves.length;
                    if(this.curves[1] < -5){
                        topDown = false;
                    }
                    if(this.curves[1] > 10){
                        topDown = true;
                    }

                    console.log('start Inter',this.interval);

                    if(topDown){
                        this.curves[index] -= 10;
                    }else{
                        this.curves[index] += 10;
                    }
                    count++;

                }, this.interval);
            },
            stopit() {
                this.stop = true;
            }

        } 
    }

</script>
