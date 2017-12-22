<template>
  <div id="app">


  </div>
</template>

<script>
let appId = '98b0de5d034c6790a26f5557ffd78c56951a15813d244204e8478bf1fea3b0e6'
import axios from "axios"

export default {
  name: 'app',
  data () {
    return {
      photos: [],
      totalPhotos: 0,
      perPage: 9,
      currentPage: 1
    }
  },
    methods:{
      fetchPhotos: function(page) {
          let options = {
                params:{
                    client_id: appId,
                    page: page,
                    per_page: this.perPage
                }
          }
          axios.get('https://api.unsplash.com/photos', options)
              .then(function(response) {
                  console.log(response)
              }, console.log)
      }
    },
    created: function(){
      this.fetchPhotos(this.currentPage)
    }
}
</script>

<style lang="sass">
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px


h1, h2
  font-weight: normal


ul
  list-style-type: none
  padding: 0


li
  display: inline-block
  margin: 0 10px


a
  color: #42b983

</style>
