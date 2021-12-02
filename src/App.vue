<template>
 <div>
  <div id="app">
      <header>
          <h1>Music</h1>
      </header>
      <main> 
          <section class="player">
              <p class="song-title"> {{current.title}}  <span> {{current.artist}} </span> </p>
              <div class="control">
              
                   <img src="./assets/PREVIOUS.png" alt="pre" class="pre" @click="pre">
                  
                  <img src="./assets/play.png" alt="play" class="play" v-if="!isPlaying" @click="play">
                  <img src="./assets/PAUSE.png" alt="pause" class="pau" v-else @click="pause">
                 <img src="./assets/NEXT.png" alt="next" class="next" @click="next">
                  
              </div>
          </section>
           <section class="playlist ">
            <div class="plylist"> <h4>Playlist</h4> </div>
            <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
              
              {{song.title}} - {{song.artist}} 
            </button>

           </section>
      </main>
      <footer></footer>
  </div>
</div>

</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      current: {},
      index: 0,
      isPlaying: false,
    
      songs: [
              {
                title: "Porque",
                artist: "Maldita",
                src: require('./assets/Porque.mp3')

              },
              {
                title: "At My Worst",
                artist: "Pink Sweat", 
                src: require('./assets/Pinksweat.mp3')

              },
              {
                title: "Cheating On You",
                artist: "Charlie Put",
                src: require('./assets/Cheating.mp3')

              },
              {
                title: "I Can't Hate You",
                artist: "Kayou", 
                src: require('./assets/Kayou.mp3')

              }
           ],
        player: new Audio()



     }

  },

  methods: {
    play (song) {
        if (typeof song.src != "undefined") {
            this.current = song;

            this.player.src = this.current.src
        }
        this.player.play();
        this.player.addEventListener('ended', function () {
            this.index++;
             if(this.index > this.songs.length - 1){
               this.index = 0;
            }
             this.current = this.songs[this.index]
            this.play(this.current)
        }.bind.this)
        this.isPlaying = true;
    },

    pause (){
      this.player.pause();
      this.isPlaying = false;
    },

    pre(){
            this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }

      this.current = this.songs[this.index]
      this.play(this.current)
    },
    next (){
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }

      this.current = this.songs[this.index]
      this.play(this.current)
    }


  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
 
  }

}
</script>

<style>
 * {
   margin: 0;
   padding: 0;
   box-sizing: border-box;
   font-family: Arial, Helvetica, sans-serif;
 }

  body{
    padding-top: 30px;
  }


 #app {
   border: 1px solid gray;
   width: 500px;
   margin:auto;
   border-radius: 10px;
   overflow: hidden;
 }

 header {
   padding: 10px 0;
   background-color: rgb(23, 23, 70);
   color: white;
   text-align: center;
   
    }


 .player{
   text-align: center;
   margin-top: 20px;
 }

 .control{
   padding: 20px 0;
   display: flex;
   align-items: center;
   justify-content: center;

 }

 .control img{
   height: 30px;
   width: auto;

 }
 

 .control img.play, img.pau{
   height: 50px;
   padding: 0 10px;
   
 }
 
.pre:active, .next:active{
  height: 29px;

 }
 
  .song-title{
    font-size: 15pt;
  }
  .song-title span{
    display: block;
    font-size: 12pt;
    font-weight: normal;
    margin-top: 3px;
    color: gray
  }

    .playlist .song{
      display: block;
      width: 100%;
      text-align: center;
      padding: 15px 0;
      font-size: 14pts;
      border: none;
    }
    .playlist .song.playing{
     background: gray;
     color: #ffffff;
    }


   .plylist {
     display: flex;
     justify-content: center;
     margin-bottom: 5px;
      
     
   }
   
   .plylist h4{
   
    background: rgb(23, 23, 70);
     color: #ffffff;
     padding: 7px;
     border-radius: 5px;
     
   }

   footer {
     height: 10px;
     background: rgb(23, 23, 70);
   }
   

  
    
</style>
