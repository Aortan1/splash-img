<template id="pagination-template">
 <div class="pagination">
   <div class="pagination__left">
     <a href="#" @click="changePage(prevPage)"  :v-show = "hasPrev">Предыдущая</a>
   </div>
   <div class="pagination__mid">
     <!--<span>{{ current }} из {{ totalPages }}</span>-->
     <ul>
       <li v-if="!hasFirst"><a href="#" @click="changePage(1)">1</a></li>
       <li v-if="!hasFirst">...</li>
       <li v-for="page in pages">
         <a href="#" @click="changePage(page)" :class="{current: current == page }">{{ page }}</a>
       </li>
       <li v-if="!hasLast">...</li>
       <li v-if="!hasLast"><a href="#" @click="changePage(totalPages)">{{totalPages}}</a></li>
     </ul>
   </div>
   <div class="pagination__right">
     <a href="#" @click="changePage(nextPage)"  :v-show = "hasNext">Следующая</a>
   </div>
 </div>
</template>

<script>

import axios from "axios"

export default {
    //name: "paginagion",
    props: {
        current: {
            type: Number,
            default: 1
        },
        total: {
            type: Number,
            default: 0
        },
        perPage: {
            type: Number,
            default: 30
        },
        pageRange: { // количество страниц пагинации с каж.стороны от текущей
            type: Number,
            default: 3
        }
    },

    computed: {
        rangeStart: function() {
          let start = this.current - this.pageRange;
          return (start>0)? start : 1
        },

        rangeEnd: function(){
          let end = this.current + this.pageRange;
          return (end<this.totalPages)? end : this.totalPages;
        },

        pages: function() {
          let pages = [];
          for(let i = this.rangeStart; i<=this.rangeEnd; i++){
              pages.push(i);
          }
          return pages;
        },

        hasFirst: function() { // есть ли в pages страница 1
          return this.rangeStart === 1
        },

        hasLast: function(){ // есть ли в pages последняя страница
          return this.rangeEnd === this.totalPages
        },


        hasPrev: function(){
          return this.current > 1;
        },
        hasNext: function() {
          return this.current<this.totalPages;
        },
        totalPages: function() {
            return Math.ceil(this.total/this.perPage)
        },
        nextPage: function(){
            return this.current<this.totalPages? this.current + 1: this.totalPages;
            //return 2;
        },
        prevPage: function(){
            return this.current>1? this.current - 1: 1;
            //return 0;
        }

    },
    methods: {
            changePage: function(page) {
                this.$emit("page-changed", page)
                //console.log(page);
            }
        }

    }


</script>


<style src="../assets/style.css"></style>

<!--<style lang="sass">-->


<!--</style>-->
