<template>
  <div class="timeline">
    <h1>Tweet</h1>
      {{ tweet.auteur }}: {{ tweet.contenu }}
  </div>
</template>

<script>
export default {
  name: 'tweet',
  props: ['tweet']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
