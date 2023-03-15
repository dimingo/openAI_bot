<template>
    <section class="relative bg-white">
    <!-- leftsection -->
    <Navigation />
        <div class="h-[500px] flex-1 bg-red-200">
            <h1>test</h1>

        </div>
    
        <div class="container flex flex-col-reverse lg:flex-row items-center pag-12  lg:mt-28">
            <div class="flex flex-1 flex-col items-center lg:items-start">


                <code
                    class=" text-green-500 flex font-bold text-3xl md:text-4 leg:text-5xl text-center lg:text-left mb-6">
                    <span class="mr-2 ">Hi, Friend</span> <img src="https://raw.githubusercontent.com/paulodhiambo/paulodhiambo/master/wave.gif"  class="w-9 h-8 rotate-45   "/></code>



                <Typewriter
                    :texts="data"
                    class="text-white" />

                <div class="flex justify-center felx-wrap gap-6">
                    <code>



            <RouterView />

            <RouterLink 
            to="/chat" class="glow-on-hover text-white font p-2">
            Let's Chat
        
        </RouterLink>
       
            
                
                   </code>
                </div>

            </div>
            <div class="flex justify-center flex-1 mb-10 md:mb-16 lg:mb-0 z-10">
                <img src="../assets/images/chatbot2.png" alt="micro illustration"
                    class="  w-3/4 h-3/4 sm:w-3/4 sm:h-3/4 md:w-3/5 md:h-3/5 rounded-xl">
            </div>
            <div
                class="hidden md:block overflow-hidden bg-back rounded-l-full absolute h-80 w-2/4 top-32 right-0 lg:-bottom-28 lg:-right-30">
            </div>

        </div>
    </section>
</template>

<script setup >
import Typewriter from '../components/Typewritter.vue'
import {ref} from 'vue'
import Navigation from './Navigation.vue';


const data = ref(['I\'m a highly advanced chatbot that uses natural language processing to understand and respond to your requests. Whether you need help with a task, want to have a casual conversation, or just need someone to listen, I\'m here for you 24/7.'])
;




</script>
<style scoped>
.glow-on-hover {
    width: 220px;
    height: 50px;
    border: none;
    outline: none;

    background: rgb(15, 24, 14);
    cursor: pointer;
    position: relative;
    z-index: 0;
    border-radius: 10px;
}

.glow-on-hover:before {
    content: '';
    background: linear-gradient(45deg, #ff0000, #ff7300, #fffb00, #48ff00, #00ffd5, #002bff, #7a00ff, #ff00c8, #ff0000);
    position: absolute;
    top: -2px;
    left: -2px;
    background-size: 400%;
    z-index: -1;
    filter: blur(5px);
    width: calc(100% + 4px);
    height: calc(100% + 4px);
    animation: glowing 20s linear infinite;
    opacity: 0;
    transition: opacity .3s ease-in-out;
    border-radius: 10px;
}

.glow-on-hover:active {
    color: #000
}

.glow-on-hover:active:after {
    background: transparent;
}

.glow-on-hover:hover:before {
    opacity: 1;
}

.glow-on-hover:after {
    z-index: -1;
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    background: #111;
    left: 0;
    top: 0;
    border-radius: 10px;
}

@keyframes glowing {
    0% {
        background-position: 0 0;
    }

    50% {
        background-position: 400% 0;
    }

    100% {
        background-position: 0 0;
    }
}
</style>


