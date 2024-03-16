<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :moviesCount="movies.length" :favouriteCount="movies.filter(c=>c.favourite).length"/>
      <Box class="search">
        <Search :updateTermHandler="updateTermHandler"/>
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter"/>
      </Box>
      <Box v-if="!movies.length && !isLoading">
        <p class="text-center fs-3 text-danger">Kinolar yo'q</p>
      </Box>
      <Box v-else-if="isLoading" class="d-flex justify-content-center">
        <button class="btn btn-primary" type="button" disabled>
          <span class="spinner-border spinner-border-sm" aria-hidden="true"></span>
          <span role="status">Loading...</span>
        </button>
      </Box>
      <MovieList
          v-else
          :movies="onFilterHandler(onSearchHandler(movies,term),filter)"
          @onToggle="onToggleHandler"
          @onRemove="onRemoveHandler"
      />
     <Box class="d-flex justify-content-center">
       <nav aria-label="pagination">
         <ul class="pagination">
           <li class="page-item" @click="this.page--"><a class="page-link" href="#">Previous</a></li>
           <li v-for="pageNum in totalPages"
               class="page-item"
               :key="pageNum"
               :class="{'active':pageNum===page}"
                @click="changePageHandler(pageNum)"
           >
             <span class="page-link">{{pageNum}}</span>
           </li>
           <li class="page-item" @click="this.page++"><a class="page-link " href="#">Next</a></li>
         </ul>
       </nav>
     </Box>
      <MovieForm @createMovie="createMovie"/>
    </div>
  </div>
</template>

<script>
import AppInfo from "@/components/app-info/AppInfo.vue";
import Search from "@/components/app-search/Search.vue";
import AppFilter from "@/components/app-filter/AppFilter.vue";
import MovieList from "@/components/movie-list/MovieList.vue";
import MovieForm from "@/components/movie-add-form/MovieForm.vue";
import axios from "axios";
import PrimaryButton from "@/ui-components/PrimaryButton.vue";
import Box from "@/ui-components/Box.vue";

export default {
  components: {
    Box,
    PrimaryButton,
    MovieForm,
    MovieList,
    AppFilter,
    AppInfo,
    Search,
  },
  data() {
    return {
      movies: [],
      term: '',
      filter: 'all',
      isLoading:false,
      limit:10,
      page:1,
      totalPages:0
    }
  },
  methods: {
   async createMovie(item) {
      try {
        const response = await axios.post('https://jsonplaceholder.typicode.com/posts',item)
        this.movies.push(response.data)
      }catch (e){
        alert(e.message)
      }
    },
    onToggleHandler({id, prop}) {
      this.movies = this.movies.map((item) => {
        if (item.id === id) {
          return {...item, [prop]: !item[prop]}
        }
        return item
      })
    },
    async onRemoveHandler(id) {
      try {
       const response= await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
        this.movies = this.movies.filter(c => c.id !== id)
      }catch (e){
        alert(e.message)
      }
    },
    onSearchHandler(arr, term) {
      if (term.length === 0) {
        return arr
      }
      return arr.filter((c) => c.name.toLowerCase().indexOf(term) > -1)
    },
    updateTermHandler(term) {
      this.term = term
    },
    onFilterHandler(arr, filter) {
      switch (filter) {
        case 'like':
          return arr.filter((c) => c.like)
        case  'viewers':
          return arr.filter((c) => c.viewers > 500)
        default:
          return arr
      }
    },
    updateFilterHandler(filter) {
      this.filter = filter
    },

    async fetchMovie() {
        try {
          this.isLoading=true
          const response = await axios.get('https://jsonplaceholder.typicode.com/posts',{
            params:{
              _limit:this.limit,
              _page:this.page
            }
          })
          this.movies=response.data.map(item => ({
            id: item.id,
            name: item.title,
            like: false,
            favourite: false,
            viewers: item.id * 50,
          }))
          this.totalPages=Math.ceil(response.headers['x-total-count']/this.limit)
        } catch (e) {
          console.log('error')
        } finally {
          this.isLoading=false
        }
    },
    changePageHandler(page){
      this.page=page
    },
  },
  mounted() {
    this.fetchMovie()
  },
  watch:{
    page(){
      this.fetchMovie()
    }
  }
}
</script>

<style scoped>
.app {
  height: 100vh;
  color: black;
}

.content {
  width: 1420px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

</style>