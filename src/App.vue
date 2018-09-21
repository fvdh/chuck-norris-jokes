<template>
  <div id="app">

    <chuckNorrisJokes @getJokes="getJokes" @toggleFavorite="toggleFavorite" :jokes="jokes" :loaded="loadedJokes"/>
    <favoriteJokes @deleteFavorite="toggleFavorite" :favorites="favorites" />


  </div>
</template>

<script>
import chuckNorrisJokes from '@/components/chuckNorrisJokes.vue'
import favoriteJokes from '@/components/favoriteJokes.vue'

import axios from 'axios';

export default {
  name: 'app',
  data(){
    return{
      loadedJokes: false,
      jokes: {},
      favorites: []
    }
  },
  components: {
    chuckNorrisJokes,
    favoriteJokes
  },
  created() {
    if( localStorage.fav.length ){
      this.favorites = JSON.parse(localStorage.getItem("fav"))
    }
  },
  methods: {
    getJokes: function(){
      const vm = this;
      vm.jokes = {}
      axios.get(`http://api.icndb.com/jokes/random/10`).then(response => {
          vm.jokes = response.data.value;
          vm.loadedJokes = true;
        })

    },
    checkFavorites: function(e){
      var vm = this;

      for(var i=0; i < vm.favorites.length; i++){
        if( vm.favorites[i].id == e){
          vm.favorites.splice(i, 1)
          this.setLocalStorage()
          return true
        }
       }
       return false
    },
    toggleFavorite: function(id, val, index){
      var vm = this;

      if( this.checkFavorites(id) == false ){
        this.favorites.push({'id': id, 'joke': val})
        vm.jokes.splice(index, 1)

        this.setLocalStorage()

      }

    },
    setLocalStorage: function(){
      var favorites = this.favorites;
      localStorage.setItem("fav", JSON.stringify(favorites));
    }
  }
}
</script>

<style lang="less">
*, ::before, ::after{
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

button:focus{
  outline: none;
}

#app{
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 100vh;
  > div{
    overflow: auto;
  }
}

header{
  height: 50px;
  width: 90%;
  max-width: 750px;
  margin: 50px auto 0 auto;
  display: flex;
  justify-content: space-between;
  h1{
    margin: 0;
    line-height: 50px;
    font-size: 22px;
    letter-spacing: 0.075em;
    font-weight: 400;
  }
}

@media screen and (max-width: 1300px){
  #app{
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;
    > div{
      padding-bottom: 100px;
      overflow: inherit;
    }
  }
}

</style>
