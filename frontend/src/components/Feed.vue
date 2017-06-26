<template>
  <div class="timeline">
    <ul v-for="tweet in tweets">
      <li>
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

</style>
