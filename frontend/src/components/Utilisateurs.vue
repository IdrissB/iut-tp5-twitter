<template>
  <div class="utilisateurs">
    <select id="utilisateur" @change="onChange($event.target.value)">
      <option disabled value="">Choisissez un utilisateur ...</option>
      <option v-for="utilisateur in utilisateurs" :value="utilisateur.handle">
      {{ utilisateur.prenom }} {{ utilisateur.nom }}
      </option>
    </select>
  </div>
</template>

<script>
import Vue from 'vue'
import Resource from 'vue-resource'
Vue.use(Resource)
export default {
  name: 'utilisateurs',
  props: ['utilisateurs'],
  methods: {
    changeUser: function (handle) {
      this.$emit('changeUser', handle)
    }
  }
}
</script>
