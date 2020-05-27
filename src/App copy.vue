<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    <main>
      <section class="player">
          <h2 class="song-title">{{ current.title }}- <span>{{ current.artist }}</span></h2>
          <div class="control">
            <button class="prev" @click="prev">Prev</button>
            <button class="play"  v-if="!isplaying" @click="play">Play</button>
            <button class="pause" v-else @click="pause">Pause</button>
            <button class="next" @click="next">Next</button>
          </div>
      </section>
      <section class="playlist">
       <h3>The PlayList</h3>
       <button v-for="song in songs" :key="song.src" @click="play(song)" :class="song.src == current.src ? 'song playing' : 'song'">
         {{ song.title }}-{{ song.artist }}
       </button>
      </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      current: {},
      index: 0,
      isplaying: false,
      songs: [
        {
          title: 'Grateful',
          artist: 'Neffex',
          src: require('./assets/track_02.mp3')
        },
        {
          title: 'Invencible',
          artist: 'Def Kob',
          src: require('./assets/track_03.mp3')
        }
      ],
      player: new Audio()
    }
  },

  methods: {
    play (song) {
      if(typeof song.src !="undefined"){
        this.current.song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.ispalying = true; 
  },

    pause(){
      this.player.pause();
      this.ispalying = false;
    },
     next(){
      this.index++;
      if(this.index > this.songs.length -1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev(){
      this.index--;
        if(this.index <0){
          this.index = this.songs.length -1;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
    }
  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: sans-serif;
}
header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  background-color: #212121;
  color: #fff;
}
</style>
