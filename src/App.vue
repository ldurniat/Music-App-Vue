<script setup>
import { reactive, ref, onMounted } from 'vue'

let index       = 0
let player      = new Audio()
const isPlaying = ref(false)
const current   = reactive({})
const songs     = [
    { 
        title: 'Grateful', 
        artist: 'Neffex', 
        src: '/assets/neffex-grateful.mp3'
    },
    { 
        title: 'Invincible', 
        artist: 'Deaf-Kev', 
        src: '/assets/deaf-kev-invincible.mp3'
    }
]
function created() {
    current.value = songs[index]
    player.src    = current.value.src
    //player.play()
}

function play(song) {
    console.log(song.src)
    if(typeof song.src != "undefined"){
        current.value = song

        player.src = current.value.src
    }

    player.play()
    player.addEventListener('ended', function(){
        next()
    })
    isPlaying.value = true
}

function pause() {
    player.pause()
    isPlaying.value = false
}

function previous() {
    index--
    if(index < 0){
        index = songs.length - 1
    }

    current.value = songs[index]
    play(current.value)
}

function next() {
    index++
    if(index > songs.length - 1){
        index = 0
    }

    current.value = songs[index]
    play(current.value)
}

onMounted(created)
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
            <div class="controls">
                <button class="prev" @click="previous">Previous</button>
                <button class="play" v-if="!isPlaying" @click="play">Play</button>
                <button class="pause" v-else @click="pause">Pause</button>
                <button class="next" @click="next">Next</button>
            </div>
        </section>
        <section class="playlist">
            <h3>The Playlist</h3>
            <button 
                v-for="song in songs" 
                :key="song.src" 
                @click="play(song)" 
                :class="(song.src == current.src) ? 'song playing' : 'song'"
            >
            {{ song.title }} - {{ song.artist }}
            </button>
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
main {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    padding:  25px;
}

.song-title {
    color: #53565A;
    font-size: 32px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
}
.song-title span {
    font-weight: 400;
    font-style: italic;
}
.controls {
    display: flex;
    justify-content: center;
    padding: 30px 15px;
}
button {
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
}
.play {
    font-size: 20px;
    font-weight: 700;
    padding: 15px 25px;
    margin: 0px 15px;
    border-radius: 8px;
    color: #FFF;
    background-color: #CC2E5D;
}
</style>
