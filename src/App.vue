<script setup>
import { reactive, ref } from 'vue'

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
    player.value  = current.value.src
    player.play()
}

function play(song) {
    console.log(song.src)
    if(typeof song.src != "undefined"){
        current.value = song

        player.src = current.src
    }

    player.play()
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
</style>
