<template>
  <div class="timeline">
    <h1>Liste de tweets</h1>
    <ul v-for="tweet in tweets">
      <li>
      {{ tweet }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'timeline',
  data () {
    return {
      tweets: ['tweet 1', 'tweet 2', 'tweet 3']
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  margin: 0 10px;
}
</style>
