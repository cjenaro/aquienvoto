<template>
  <section class="main">
    <div v-for="candidate in candidates" v-bind:key="candidate.id" class="candidate">
      <div class="candidate-logo"></div>
      <h1 class="name">{{ candidate.name }}</h1>
      <div class="news" v-for="article in candidate.news" v-bind:key="article.title">
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
          name: 'Mario+Negri',
          partido: 'Cordoba cambia',
          news: [],
        },
        {
          id: 2,
          name: 'Juan+Schiaretti',
          partido: 'Hacemos por Cordoba',
          news: [],
        },
        {
          id: 3,
          name: 'Fernando+Schülle',
          partido: 'Partido humanista',
          news: [],
        },
        {
          id: 4,
          name: 'Aurelio+Elorrio',
          partido: 'Encuentro Vecinal Cordoba',
          news: []
        },
        {
          id: 5,
          name: 'Carlos+Bianco',
          partido: 'Union del centro democratico',
          news: []
        },
        {
          id: 6,
          name: 'Enrique+Sella',
          partido: 'P.A.I.S',
          news: []
        },
        {
          id: 7,
          name: 'Ramón+Mestre',
          partido: 'Union civica radical',
          news: []
        },
        {
          id: 8,
          name: 'Liliana+Olivero',
          partido: 'Frente de izquierda y de los trabajadores',
          news: []
        },
        {
          id: 9,
          name: 'Eduardo+Mulhall',
          partido: 'Movimiento avanzada socialista',
          news: []
        },
        {
          id: 10,
          name: 'Kasem+Dandach',
          partido: 'Movimiento de accion vecinal',
          news: []
        },
        {
          id: 11,
          name: 'Luis+Beltrán',
          partido: 'Vecinalismo Independiente',
          news: []
        },
        {
          id: 12,
          name: 'Agustín+Spaccesi',
          partido: 'Partido Unión Ciudadana',
          news: []
        },
        {
          id: 13,
          name: 'Luciana+Echevarría',
          partido: 'MST-Nueva Izquierda',
          news: []
        }
      ]
    }
  },
  mounted() {
    for (let i = 0; i < this.candidates.length; i++) {
      axios.get('https://newsapi.org/v2/everything?q=' + this.candidates[i].name + '&domains=clarin.com,perfil.com,lanacion.com.ar,lavoz.com.ar,pagina12.com.ar&apiKey=4483c32148994e428926ebdd2294ac9a')
          .then(response => {
            this.candidates[i].news = response.data.articles;
            })
          .catch(error => {console.log(error);})
          .finally()
    }
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
