<template lang="html">
  <div>
    <h2>{{anime.title}}</h2>
    <img v-bind:src="anime.image_url">
    <p>Synopsis: {{anime.synopsis}}</p>
    <p>Rank: #{{anime.rank}}</p>
    <p>Number of Episodes: {{anime.episodes}}</p>
    <p>Rating: {{anime.score}}/10</p>
    <p>Popularity: #{{anime.popularity}}</p>
    <p>Views: {{anime.members}}</p>
  </div>
</template>

<script>
export default {
  name: "anime-details",
  props: ['anime']
}
</script>

<style lang="css" scoped>
img{
  height: 250px;
}
</style>
