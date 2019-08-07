<template>
  <main>
    <pm-notification v-show="showNotification" v-bind:typeNotification="hasData">
      <p slot="body" v-if="hasData">No se encontraron resultados</p>
      <p slot="body" v-else>{{ searchMessage }}</p>
    </pm-notification>
    <pm-loader v-show="isLoading"></pm-loader>
    <section class="section" v-show="!isLoading">
      <nav class="nav">
        <div class="container">
          <input class="input is-large" type="text" placeholder="Buscar Canciones" v-model="searchQuery" v-on:keyup.enter="search">

          <a class="button is-info is-large" v-on:click="search">Buscar</a>
          <a class="button is-danger is-large">&times</a>
        </div>
      </nav>

      <div class="container results">
        <div class="columns is-multiline">
          <div class="column is-one-quarter" v-for="t in tracks">
            <pm-track v-bind:track="t" 
            v-blur="t.preview_url"
            v-bind:class="{ 'is-active': t.id == selectedTrack }" 
            v-on:select="setSelectedTrack"></pm-track>
             
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>

import trackService from '@/services/track.js'

import PmTrack from '@/components/Track.vue'

import PmNotification from '@/components/shared/notification.vue'
import PmLoader from '@/components/shared/Loader.vue'

export default {
  name: 'app',

  components: { PmTrack, PmLoader, PmNotification },

  data () {
    return {
      searchQuery: '',
      tracks: [],

      isLoading: false,
      showNotification: false,
      hasData: false,
      selectedTrack: '',
    }
  },

  computed:{
    searchMessage(){
      return "Resultados encontrados:" + this.tracks.length;
    }
  },

  watch: {
    showNotification (){
      if(this.showNotification){
        setTimeout(() =>{
          this.showNotification = false
        }, 3000)
      }
    }
  },

  methods: {
    search(){
      if(!this.searchQuery) { return }

      this.isLoading = true

      trackService.search(this.searchQuery)
        .then(res =>{
          this.showNotification = true
          this.hasData = res.tracks.total === 0
          this.tracks = res.tracks.items
          this.isLoading = false
        })
    },

    setSelectedTrack(id){
      this.selectedTrack = id
    }

  }
}
</script>



<style lang="scss">
  .results{
    margin-top: 50px;
  }

  .is-active{
    border: 3px #23d160 solid;
  }
</style>
