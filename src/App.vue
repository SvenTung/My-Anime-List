<template>
  <div id="all-content">
    <div id="header">
      <div id="search-bar-area">
        <label for="search_bar">Search:</label>
        <input type="text" name="search_bar" id="search-bar" v-model="searchTerm">
        <button type="button" name="search" v-on:click="handleButtonClick">Search</button>
      </div>
      <h1><u>My Anime List</u></h1>
    </div>

    <div id="genre-bar">
      <genre-list></genre-list>
    </div>

    <div id='main-content'>

      <div id='top-20-ranked-anime' v-if="filter == ''">
        <h3>Top 20 ranked anime</h3>
        <anime-list :animes='topRankedAnimes'></anime-list>
      </div>

      <div id='anime-list' v-if="filter != ''">
        <h2>{{this.filter}}</h2>
        <anime-list :animes='animeList'></anime-list>
      </div>

      <div id='animeDetails' v-if="selectedAnime">
        <anime-details :anime='selectedAnime'></anime-details>
      </div>

    </div>

  </div>
</template>

<script>
import AnimeList from './components/AnimeList.vue';
import GenreList from './components/GenreList.vue';
import AnimeDetails from './components/AnimeDetails.vue';
import {eventBus} from './main.js';

export default {
  name: 'app',
  data(){
    return{
      topRankedAnimes: [],
      selectedAnime: null,
      selectedGenre: null,
      animeList: [],
      searchTerm: "",
      filter: ""
    };
  },
  methods: {
    handleButtonClick(){
      this.filter = this.searchTerm
      fetch("https://api.jikan.moe/v3/search/anime?q=" + this.searchTerm)
      .then(response => response.json())
      .then((animeList) =>{
        this.animeList = []
        for (var i = 0; i < 20; i++) {
          this.animeList[i] = animeList.results[i]
        }
      });
    }
  },
  components: {
    "anime-list": AnimeList,
    "genre-list": GenreList,
    "anime-details": AnimeDetails
  },
  mounted() {
    fetch("https://api.jikan.moe/v3/top/anime/1/favorite")
    .then(response => response.json())
    .then((topAnimes) =>{
      this.topRankedAnimes = []
      for (var i = 0; i < 20; i++) {
        this.topRankedAnimes[i] = topAnimes.top[i]
      }
    });

    eventBus.$on ('selected-anime', (anime_id) => {
      fetch("https://api.jikan.moe/v3/anime/" + anime_id)
      .then(response => response.json())
      .then((selectedAnime) =>{
        this.selectedAnime = selectedAnime
      })
    });

    eventBus.$on ('selected-genre', (genre) => {
      this.selectedGenre = genre
      this.filter = genre.name
      console.log(genre.id);
      fetch("https://api.jikan.moe/v3/search/anime?genre=" + genre.id)
      .then(response => response.json())
      .then((animeList) =>{
        this.animeList = []
        for (var i = 0; i < 20; i++) {
          this.animeList[i] = animeList.results[i]
        }
      })
    });
  }
}
</script>

<style>
#header{
  background-color: #A03131;
  padding: 8px;
}

#search-bar-area{
  display: flex;
  float: right;
}

#search-bar{
  margin-left: 10px;
  margin-right: 10px;
}

#main-content{
  display: flex;
  justify-content: space-around;
}

#animeDetails{
  width: 50%;
}

#genre-bar{
  background-color: #4F7CAC
}

</style>
