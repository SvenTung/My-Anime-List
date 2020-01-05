<template lang="html">
  <div>
    <li v-on:click="handleListClick">{{genre.name}}</li>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
  name: "genre-list-item",
  props: ['genre'],
  methods: {
    handleListClick(){
      eventBus.$emit('selected-genre', this.genre)
    }
  }

}
</script>

<style lang="css" scoped>
li{
  list-style: none;
  display: inline-block;
  padding: 14px 16px;
  color: white;
}
li:hover{
  background-color: #304B68;
}
</style>
