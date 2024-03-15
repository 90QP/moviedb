<template>
  <div>
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form action="" class="search-box" v-on:submit.prevent="handleSearch">
        <input 
          type="search" 
          placeholder="Search for a movie..."
          v-model.lazy="search_query"
          required
        >
      </form>
    </header>

    <main>
      <div class="cards" v-if="movieList.length > 0">
        <!-- {{ movieList[0].title }}
        {{ movieList[0].overview }} -->
        <Card v-for="movie in movieList" v-bind:aa="movie"/>
        <!-- aa라는 이름으로 movie값이 전달됨. movie는 movieList(배열)에서 foreach로 받아온 하나하나의 값임!-->
      </div>
      <div class="no-result" v-else>
        <h3>'{{search_query}}'의 검색 결과가 없습니다.</h3>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Card from './components/Card.vue';

const movieList = ref([]);
const search_query = ref('');


const handleSearch = async () => {
  movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${search_query.value}&include_adult=false&language=ko-KR&page=1&api_key=682c3bea67555225eb17737fdaee18cc`)
  .then(response => response.json())
  .then(response => response.results)

  console.log('받아온 데이타는' , movieList.value) 
  //promise..비동기함수??? 라서 async와 await 사용 => proxy로 뜸
}


//화면이 시작되면 인기작들을 표시
const popular = async () => {
  movieList.value = await fetch('https://api.themoviedb.org/3/discover/movie?include_adult=false&include_video=false&language=ko-KR&page=1&api_key=682c3bea67555225eb17737fdaee18cc')
  .then(response => response.json())
  .then(response => response.results)


  console.log('받아온 데이타는' , movieList.value) 
  //promise..비동기함수??? 라서 async와 await 사용 => proxy로 뜸
}
popular();


</script>

<style lang="scss" scoped>
@font-face {
    font-family: 'LINESeedKR-Rg';
    src:url('https://cdn.jsdelivr.net/gh/wizfile/font/LINESeedKR-Rg.woff') format('woff');
    font-style: normal;
}

  $color:#313131;
  $green:#a1cab1;

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;

    font-family: 'LINESeedKR-Rg',sans-serif;
  }

  header {
    padding: 50px 0;

    h1 {
      color:#767676;
      font-size: 42px;
      font-weight: 100;
      text-align: center;
      margin-bottom: 30px;
      text-transform: uppercase;

      strong {
        color: $color;
      }
    }

    .search-box {
      display: flex;
      justify-content: center;

      input {
        appearance: none;
        border: none;
        outline: none;
        background: #f3f3f3;
        font-size: 18px;
        color: $color;
        transition: 0.3s;

        padding: 20px 15px 15px;
        width: 100%;
        max-width: 600px;
        border-radius: 8px;
        box-shadow: 0 2px 6px rgba(0,0,0,0.1) ;

        &::placeholder {
          color: rgba(0,0,0,0.4);
        }

        &:focus {
          background: #a1cab1;
        }
      }
    }
  }

  main {
    max-width: 1250px;
    margin: auto;
    background-color: #f9f9f9;
    border-radius: 16px;
    padding: 10px;

    .cards {
      
      display: flex;
      flex-wrap: wrap;
    }

    .no-result {
      padding: 50px 0;
      text-align: center;
    }
  }
</style>