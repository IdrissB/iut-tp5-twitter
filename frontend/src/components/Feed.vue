<template>
  <div class="timeline">
    <ul v-for="tweet in tweets">
      <li class="tweet">
        <tweet :tweet="tweet"/>
      </li>
    </ul>
  </div>
</template>

<script>
import Tweet from './Tweet'
export default {
  name: 'feed',
  components: {Tweet},
  props: ['tweets']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li.tweet:first-child {
 border-top-width: 1px;
}

li.tweet {
 border-style: solid;
 border-width: 0 1px 1px 1px;
 border-color: gray;
 width: 500px;
 margin: auto;
}
</style>
