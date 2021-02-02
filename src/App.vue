<template lang="pug">
.app
  header
    h1 The
      strong Anime
      | Search
    
    form.search-box(@submit.prevent="HandleSearch")
      input(type="text"
            placeholder="rechercher un anime..." 
            required
            v-model="search_query").search-field
  
  main
    .cards(v-if="animeList.length > 0")
       Card(v-for="anime in animeList" 
					:key="anime.mal_id"
					:anime="anime")
    
    .no-results(v-else)
      h3 Désolé, nous avons pas de resultats..


</template>

<script>
import { ref } from 'vue'
import Card from './components/Card'

export default {
  setup(){
    const search_query = ref("");
    const animeList = ref([]);

    const HandleSearch = async () => {
      animeList.value = await fetch(`https://api.jikan.moe/v3/search/anime?q=${search_query.value}`)
              .then( res => res.json())
              .then( data => data.results);
              
      search_query.value = "";
    }

    return {
      Card,
      search_query,
      animeList,
      HandleSearch
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}

a {
  text-decoration: none;
  display: inline-block;
}
header {
  padding: 50px 0;

  h1 {
    color: #e5e5e5;
    font-size: 42px;
    font-weight: 400;
    text-align: center;
    text-transform: uppercase;
    margin-bottom: 30px;
    transition: .5s ease-in;

    strong {
      color: #2E51A2;
    }

    &:hover {
      color:#2E51A2;
    }
  }

  .search-box {
    display: flex;
    justify-content: center;
    padding: 0 30px;

    .search-field {
      appearance: none;
      background: none;
      border: none;
      outline: none;

      background-color: #f3f3f3;
      box-shadow: 0 4px 8px rgba(0, 0, 0, .15);

      display: block;
      width: 100%;
      max-width: 600px;
      padding: 15px;
      border-radius: 8px;

      color: #313131;
      font-size: 20px;

      transition: .5s ease-in;

      &::placeholder {
        color: #AAA;
      }

      &:focus, &:valid {
        color: #fff;
        background: linear-gradient(to right,#2E51A2,#1B7AC2);
        box-shadow: 0 0 0 rgba(0, 0, 0, .15);
        transition: .5s ease-in;
      }
    }
  }
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 30px;
  padding-right: 30px;

  .cards {
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
  }
}
</style>
