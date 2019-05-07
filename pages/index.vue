<template>
  <section class="main">
    <div v-for="candidate in candidates" v-bind:key="candidate.id" class="candidate">
      <div class="candidate-logo"></div>
      <h1 class="name">{{ candidate.name }}</h1>
      <div class="news" v-for="article in candidate.articles" v-bind:key="article.title">
        {{ article.content }}
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      candidates: [
        {
          id: 1,
          name: 'Negri',
          news: [],
        },
        {
          id: 2,
          name: 'Schiaretti',
          news: [],
        }
      ]
    }
  },
  mounted() {
    axios.get('https://newsapi.org/v2/everything?q=Mario+Negri+2019&apiKey=4483c32148994e428926ebdd2294ac9a')
         .then(response => {
           this.candidates[0].news = response.data.articles})
         .catch(error => {console.log(error);})
         .finally()
  },
  components() {
    
  }
}
</script>

<style>
.main {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 15px;
}

.candidate-logo {
  background-image: url('https://picsum.photos/32/32');
  width: 32px;
  height: 32px;
}
</style>
