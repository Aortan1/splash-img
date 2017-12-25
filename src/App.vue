<template>
  <div id="app">
    <pagination :current="currentPage"
                :total="totalPhotos"
                :perPage="perPage"
                @page-changed="fetchPhotos"></pagination>
    <section class="grid">
      <div class="grid__item card" v-for="photo in photos">
        <div class="card__body">
          <a :href="photo.urls.full" target="_blank">
            <img :src="photo.urls.small" alt="">
          </a>
        </div>
        <div class="card__footer media">
          <img :src="photo.user.profile_image.small" alt="" class="media__obj">
          <div class="media__body">
            <a :href="photo.user.portfolio_url" target="_blank">{{ photo.user.name }}</a>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
let appId = '98b0de5d034c6790a26f5557ffd78c56951a15813d244204e8478bf1fea3b0e6'
import axios from "axios"
import Pagination from './components/Pagination.vue'

export default {
  name: 'app',
  components: {Pagination},
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
                  //that.totalPhotos = parseInt(response.headers.get('x-total')) // общее кол-во фоток на сервере - в заголовке 'x-total' (=~49150)
                  that.totalPhotos = parseInt(response.headers['x-total'])
                   //that.totalPhotos = 49150;
                  console.log("that.totalPhotos = ",that.totalPhotos)
                  console.log("response.headers = ",response.headers)

                  that.currentPage = page
              }, console.log)
      }
    },
    created: function(){
      this.fetchPhotos(this.currentPage)
    }
}
</script>


<style src="./assets/style.css"></style>

<!--<style lang="sass">-->


<!--</style>-->
