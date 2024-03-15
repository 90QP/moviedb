<template>
  <div class="card">
    <a :href="'https://www.themoviedb.org/movie/' + aa.id">
      <figure>
        <img v-if="aa.poster_path" v-bind:src="`https://media.themoviedb.org/t/p/w300_and_h450_face/${aa.poster_path}`" :alt="aa.title">
        <img v-else src="https://placehold.it/300x450/ddd/333?text=MoviePoster" alt="포스터 없음">
      </figure>
      <div class="text">
        <h3>{{ aa.title }}</h3>
      </div>
    </a>
  </div>
</template>

<script setup>
  const props = defineProps(['aa']) ; //옵션 없을 때
</script>

<!-- <script>
  export default {
    props:['aa']
  }
</script> -->

<style lang="scss" scoped>

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;

    font-family: 'LINESeedKR-Rg',sans-serif;
  }

  a {
    text-decoration: none;
    color: inherit;
  }

  .card {
    width:20%;
    padding: 12px 16px;

    @media (max-width:1200px) {
      width: 25%;
    }
    @media (max-width:950px) {
      width: 33.33%;
    }
    @media (max-width:550px) {
      width: 50%;
    }

    a {
      display: block;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 0 7px rgba(0,0,0,0.3);

      figure {
        width: 100%;
        height: 0;
        padding-bottom: 150%;
        /* 이미지가 잘리지 않고 가로 길이에 따라 height가 함께 줄어들음  = 모든 이미지의 사이즈가 동일해서 가능 */
        border-radius: 16px 16px 0 0;
        overflow: hidden;

        img {
          width : 100%;
          transition: 0.3s;
        }
      }
      
      .text {
        padding: 20px 16px;
        background: #fff;

          h3 {
            color:#111;
            transition: 0.3s;
            font-size: 20px;

            @media (max-width:950px) {
              font-size: 18px;
            }
          }
        }

      &:hover img{
          transform: scale(1.05)
      }
      &:hover h3 {
        color:#06965a;
      }
    }
  }
</style>