<template>
  <div id="app">
    <p v-if="isLoading">Loading</p>
    <search v-on:SearchRequested="handleSearch"></search>
    <preview :gifs=gifs></preview>
  </div>
</template>


<script>
import Search from './components/Search.vue'
import Preview from './components/Preview.vue'

export default {
  name: 'app',
  data(){
    return{
      isLoading: true,
      gifs:[]
    }
  },
  methods: {
    doQuery(url){
      fetch(url)
      .then((res)=>{  return res.json();  })
      .then((res)=>{  
        this.gifs = res.data;  
        this.isLoading = false;
      })
    },
    handleSearch(query){
      this.gifs = [];
      this.isLoading = true;
      const url = `http://api.giphy.com/v1/gifs/search?q=${query}&api_key=ylvFwK38nwRNgzj2rUPw5QzdHH8xIfst` ;
      this.doQuery(url);
    }
  },
  components: {  Search, Preview  },
  created() {
    fetch('http://api.giphy.com/v1/gifs/trending?api_key=ylvFwK38nwRNgzj2rUPw5QzdHH8xIfst')
      .then((res)=>{  return res.json();  })
      .then((res)=>{  
        this.gifs = res.data;  
        this.isLoading = false;
      })
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
