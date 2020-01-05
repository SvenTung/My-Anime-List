<template lang="html">
  <div>
    <ul id="genre-list">
      <genre-list-item v-for="(genre, index) in this.genres" :genre="genre" :index="index"></genre-list-item>
    </ul>
  </div>

</template>

<script>
import GenreListItem from './GenreListItem.vue';

export default {
  name: 'genre-list',
  data(){
    return{
      genres: [{name:"Action", id:"1"}, {name:"Adventure", id:"2"}, {name:"Comedy", id:"4"}, {name:"Demons", id:"6"}, {name:"Mystery", id:"7"}, {name:"Fantasy", id:"10"}, {name:"Horror", id:"14"}, {name:"Magic", id:"16"}, {name:"Mecha", id:"18"}, {name:"Romance", id:"22"}, {name:"School", id:"23"}, {name:"Sci Fi", id:"24"}, {name:"Space", id:"29"}, {name:"Supernatural", id:"37"}]
    }
  },
  components: {
    "genre-list-item": GenreListItem
  }

}
</script>

<style lang="css" scoped>
ul{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  margin: 0px;
  padding: 0px;
}

</style>
