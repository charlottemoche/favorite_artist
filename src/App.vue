<template>
  <div id="app">
  <h1>Enter your favorite artist!</h1>
  <input type="text" v-model="artist" value=" ">
  <button v-on:click="searchArtist()">search</button>
    <p>
        <!-- {{ list.strArtist }} -->
        <br>
        <img :src="list.strArtistThumb" alt="" width=30%>
    </p>
  </div>
</template>

<script>
import axios from "axios"
const baseUrl = "https://www.theaudiodb.com/api/v1/json/2/search.php?s=";

export default {
  name: "App",

  data()
  {
    return {
      list: [],
      artist: "",
    }
  },

  // async mounted()
  // {
  //   let result = await axios.get(`${baseUrl}`);
  //   console.log(result.data.artists[0]);
  //   this.list = result.data.artists[0];
  // },

  methods: {
    searchArtist: function() {
      var artist = this.artist;
      axios
        .get(`${baseUrl}${artist}`)
        .then(result => {
          console.log(result.data.artists[0]);
          this.list = result.data.artists[0];
        })
        .catch(error => {
          this.errors = error.result.data.errors;
        });
    },
    showArtist: function() {
      
    }
  }
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif; 
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  text-align: center;
  margin: 0;
  position: absolute;     
  top: 50%;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -50%);
  padding: 4em;
  background: white;
  /* opacity: .8; */
  border-radius: 10px;
}

body {
  background: lightblue;
}


</style>
