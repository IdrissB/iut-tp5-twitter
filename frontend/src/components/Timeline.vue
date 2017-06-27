<template>
  <div class="timeline">
    <h1>Liste de tweets</h1>
    <feed :tweets="tweets" @retweeted="retweet" :loading="loading"></feed>
    </p>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
var tweet1 = {auteur: 'Idriss', contenu: 'Bonjour Twitter'}
var tweet2 = {auteur: 'Michel', contenu: 'La canicule c\'est chaud'}
var tweet3 = {auteur: 'Jean', contenu: 'Alexandra tu arrêtes maintenant'}
import Feed from './Feed'
export default {
  // permet d'utiliser feed dans le template
  components: {Feed},
  name: 'timeline',
  data () {
    return {
      loading: true,
      tweets: [tweet1, tweet2, tweet3]
    }
  },
  created () {
    this.fetchTweets()
  },
  methods: {
    fetchTweets: function () {
       // GET /someUrl
      this.$http.get('http://localhost:8080/list').then(response => {
        // get body data
        this.tweets = response.body
        this.loading = false
      }, response => {
          // error callback
      })
    },
    retweet: function (id) {
      var tweet = this.tweets.find(tweet => id === tweet.id)
      tweet.retweeters.push({handle: 'johndoe'})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
