<script setup>
import { reactive } from 'vue'

let index     = 0
let player    = new Audio()
const current = reactive({})
const songs   = [
    { 
        title: 'Grateful', 
        artist: 'Neffex', 
        src: require('./assets/neffex-grateful.mp3')
    },
    { 
        title: 'Invincible', 
        artist: 'Deaf-Kev', 
        src: require('./assets/deaf-kev-invincible.mp3')
    }
]
function created() {
    current.value = songs[index]
    player.value  = current.value.src
    player.play()
}
</script>

<template>
    <header>
        <h1>My Music</h1>
    </header>
    <main>
        <section class="player">
            <h2 class="song-title">{{ current.title}} -
                <span>
                    {{ current.artist }}
                </span>
            </h2>
        </section>
    </main>
</template>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: 0;
}
body {
    font-family: sans-serif;
}
header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #FFF; 
}
</style>
