<template id="pagination-template">
 <div class="pagination">
   <div class="pagination__left">
     <a href="#" @click="changePage(prevPage)">Предыдущая</a>
   </div>
   <div class="pagination__right">
     <a href="#" @click="changePage(nextPage)">Следующая</a>
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
        }},

    computed: {
        nextPage: function(){
            return this.current + 1;
            //return 2;
        },
        prevPage: function(){
            return this.current - 1;
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
