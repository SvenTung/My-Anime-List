<template lang="html">
  <div>
    <ul>
      <anime-list-item v-for="(anime, index) in animes" :anime="anime" :index="index"></anime-list-item>
    </ul>
  </div>

</template>

<script>
import AnimeListItem from './AnimeListItem.vue';

export default {
name: 'anime-list',
props: ['animes'],
components: {
  "anime-list-item": AnimeListItem
}

}
</script>

<style lang="css" scoped>
ul{
  padding: 0px;
}
</style>
