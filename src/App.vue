<template lang="pug">
  #app
    img(src='/assets/logo.png')
    h1 PlatziMusic
    select(v-model="selectedCountry") 
      option(v-for="country in countries" v-bind:value="country.value") {{country.name}}
    spinner(v-show="loading")
    ul
      artist(v-for="artist in artists" v-bind:artist="artist" :key="artist.mbid")

</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        {name: 'Agentina', value: 'argentina'},
        {name: 'Colombia', value: 'colombia'},
        {name: 'España', value: 'spain'},
      ],
      selectedCountry: 'spain',
      loading: true  
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods:{
    refreshArtist(){
      const self = this
      this.loading=true
      this.artists= []
      getArtists(this.selectedCountry)
        .then(function (artists) {
          self.loading = false
        self.artists = artists
      })

    }
  },
  mounted: function(){
    this.refreshArtist()
  },
  watch:{
    selectedCountry: function (){
      this.refreshArtist()
    }
  }
}
</script>

<style lang="stylus" >
#app
    font-family 'Montserrat', sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px

h1, h2
    font-weight normal

ul
    list-style-type none
    padding 0
    display flex
    flex-wrap wrap
    justify-content center

li
    display inline-block
    margin 0 10px
    
</style>
