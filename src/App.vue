<template>
  <div id="app">
    <div v-for="photo in photos" style="display: inline-block;">
      <img :src="photo.urls.small" alt="">
    </div>

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
      perPage: 30,
      currentPage: 1
    }
  },
    methods:{
      fetchPhotos: function(page) {
          let that = this;
          let options = {
                params:{
                    client_id: appId,
                    page: page,
                    per_page: this.perPage
                }
          }
          axios.get('https://api.unsplash.com/photos', options)
              .then(function(response) {
                  console.log(response.data)
                  that.photos = response.data
                  that.totalPhotos = parseInt(response.headers.get('x-total'))
                  that.currentPage = page
              }, console.log)
      }
    },
    created: function(){
      this.fetchPhotos(this.currentPage)
    }
}
</script>

<style lang="sass">


</style>
