<template>
  <li>
    <h2>
      <a v-bind:href="artist.url" target="_blank">{{artist.name}}</a>
      <img v-bind:src="artist.image[2]['#text']" />
    </h2>
  </li>
</template>

<script>
export default {
  name : 'artist',
  props : ['artist']
}
</script>

<style scoped>
ul {
  list-style-type: none;
  display: block;
  margin: 10px;
  padding: 0;
}
</style>