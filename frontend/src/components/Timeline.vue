<template>
  <div class="timeline">
    <h1>Liste de tweets</h1>
    <feed :tweets="tweets" @retweeted="retweet" :utilisateur="currentUser" :loading="loading"></feed>
    <h1>Liste utilisateurs</h1>
    <utilisateurs :utilisateurs="utilisateurs" @utilisateurChanged="changeUser" ></utilisateurs>
    </p>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
import Utilisateurs from './Utilisateurs'
Vue.use(Resource)
import Feed from './Feed'
export default {
  // permet d'utiliser feed dans le template
  components: {Feed, Utilisateurs},
  name: 'timeline',
  data () {
    return {
      loading: true,
      tweets: [],
      utilisateurs: [],
      currentUser: null
    }
  },
  created () {
    this.fetchTweets()
    this.fetchUtilisateurs()
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
    },
    fetchUtilisateurs: function () {
      console.log('ici')
       // GET /someUrl
      this.$http.get('http://localhost:8080/utilisateurs').then(response => {
      // get body data
        this.utilisateurs = response.body
        this.changeUser(this.utilisateurs[0].handle)
      }, response => {
          // error callback
      })
    },
    changeUser: function (handle) {
      for (let i = 0; i < this.utilisateurs.length; i++) {
        if (this.utilisateurs[i].handle === handle) {
          this.currentUser = this.utilisateurs[i]
          this.$http.get('http://localhost:8080/feed/' + handle).then(response => {
            this.tweets = response.body
          }, response => {
          })
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
