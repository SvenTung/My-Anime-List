<template lang="html">
  <div>
    <li v-on:click="handleListClick">{{anime.title}}</li>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: "anime-list-item",
  props: ['anime'],
  methods: {
    handleListClick(){
      eventBus.$emit('selected-anime', this.anime.mal_id)
    }
  }

}
</script>

<style lang="css" scoped>

</style>
