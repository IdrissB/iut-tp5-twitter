<template>
  <div class="timeline">
    <div>
      <strong>{{ tweet.auteur.prenom }} {{ tweet.auteur.nom }}</strong><span class="handle"> @{{ tweet.auteur.handle }} - {{ moment() }}</span>
    </div>
    <div>
       {{ tweet.contenu }}
    </div>
    <div>
      <ul>
        <li class="button"><icon name="reply"/></li>
        <li class="button"><a @click="retweet()"><icon name="retweet"/>{{ tweet.retweeters.length}}</a></li>
        <li class="button"><icon name="heart"/></li>
        <li class="button"><icon name="envelope"/></li>
      </ul>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'
export default {
  components: {Icon},
  name: 'tweet',
  props: ['tweet'],
  created () {
    moment.locale('fr')
  },
  methods: {
    moment: function () {
      return moment(this.tweet.date).fromNow()
    },
    retweet: function () {
      this.$http.get('http://localhost:8080/retweet', {params: {utilisateur: 'coldplay', tweet: this.tweet.id}, responseType: 'text'}).then(response => {
        // get body data
        this.tweets = response.body
        this.$emit('retweeted', this.tweet.id)
      }, response => {
        this.$emit('fail retweeted', this.tweet.id)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
li.button {
 display: inline-block;
}

a {
 color: #42b983;
}

span.handle {
 color: gray;
}
</style>
