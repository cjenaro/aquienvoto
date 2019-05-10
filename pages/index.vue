<template>
  <section>
    <h1 class="title">A quien voto?</h1>
    <div class="main">
      <div v-for="candidate in candidates.filter((candidate) => candidate.news.length > 0)" v-bind:key="candidate.id" class="candidate">
        <div class="candidate-logo" :style="getCandidatePic(candidate.pic)"></div>
        <div class="name-twitter-container">
          <h1 class="name">{{ candidate.name.replace("+", " ") }}</h1>
          <a :href="candidate.twitter" target="_blank" class="tw-logo"></a>
        </div>
        <div class="news" v-for="article in candidate.news" v-bind:key="article.title">
          <h3 class="news-title"> {{ article.title }} </h3>
          <p class="description"> {{ parseContent(article.content) }} </p>
          <a :href="article.url"  target="_blank" class="news-link"> Ver en el diario </a>
        </div>
      </div>
    </div>
    <footer>
      <p>Use la <a href="https://newsapi.org/" class="news-api">News API</a> para traer los articulos del diario</p>
    </footer>
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
          pic: 'aquienvoto/negri.jpg',
          twitter: 'https://twitter.com/marioraulnegri',
          news: [],
        },
        {
          id: 2,
          name: 'Juan+Schiaretti',
          partido: 'Hacemos por Cordoba',
          pic: 'aquienvoto/schiaretti.png',
          twitter: 'https://twitter.com/JSchiaretti',
          news: [],
        },
        {
          id: 3,
          name: 'Fernando+Schülle',
          partido: 'Partido humanista',
          pic: 'aquienvoto/schulle.jpg',
          twitter: 'https://twitter.com/ferschule',
          news: [],
        },
        {
          id: 4,
          name: 'Aurelio+Elorrio',
          partido: 'Encuentro Vecinal Cordoba',
          pic: 'aquienvoto/elorrio.jpg',
          twitter: 'https://twitter.com/AGarciaElorrio',
          news: []
        },
        {
          id: 5,
          name: 'Carlos+Bianco',
          partido: 'Union del centro democratico',
          pic: 'aquienvoto/negri.jpg',
          twitter: 'https://twitter.com/marioraulnegri',
          news: []
        },
        {
          id: 6,
          name: 'Enrique+Sella',
          partido: 'P.A.I.S',
          pic: 'aquienvoto/sella.jpg',
          twitter: 'https://twitter.com/SellaEnrique',
          news: []
        },
        {
          id: 7,
          name: 'Ramón+Mestre',
          partido: 'Union civica radical',
          pic: 'aquienvoto/mestre.jpg',
          twitter: 'https://twitter.com/ramonjmestre',
          news: []
        },
        {
          id: 8,
          name: 'Liliana+Olivero',
          partido: 'Frente de izquierda y de los trabajadores',
          pic: 'aquienvoto/olivero.jpg',
          twitter: 'https://twitter.com/LilianaOlivero',
          news: []
        },
        {
          id: 9,
          name: 'Eduardo+Mulhall',
          partido: 'Movimiento avanzada socialista',
          pic: 'aquienvoto/mulhall.jpg',
          twitter: 'https://twitter.com/EduardoMulhall',
          news: []
        },
        {
          id: 10,
          name: 'Kasem+Dandach',
          partido: 'Movimiento de accion vecinal',
          pic: 'aquienvoto/dandach.png',
          twitter: 'https://twitter.com/KasemDandach57',
          news: []
        },
        {
          id: 11,
          name: 'Luis+Beltrán',
          partido: 'Vecinalismo Independiente',
          pic: 'aquienvoto/negri.jpg',
          twitter: 'https://twitter.com/marioraulnegri',
          news: []
        },
        {
          id: 12,
          name: 'Agustín+Spaccesi',
          partido: 'Partido Unión Ciudadana',
          pic: 'aquienvoto/spaccesi.jpg',
          twitter: 'https://twitter.com/SpaccesiAgustin',
          news: []
        },
        {
          id: 13,
          name: 'Luciana+Echevarría',
          partido: 'MST-Nueva Izquierda',
          pic: 'aquienvoto/echevarria.jpg',
          twitter: 'https://twitter.com/LuciEchevarria',
          news: []
        }
      ]
    }
  },
  methods: {
    parseContent: (content) => {
      return content.substring(0, content.indexOf("["))
    },
    getCandidatePic: (img) => {
      return "background-image: url('" + img + "')";
    }
  },
  mounted() {
    for (let i = 0; i < this.candidates.length; i++) {
      axios.get('https://newsapi.org/v2/everything?q=' + this.candidates[i].name + '&domains=clarin.com,perfil.com,lanacion.com.ar,lavoz.com.ar,pagina12.com.ar&apiKey=4483c32148994e428926ebdd2294ac9a')
          .then(response => {
            this.candidates[i].news = response.data.articles.slice(0, 5);
            })
          .catch(error => {console.log("ERROR", error);})
          .finally()
    }
  }
}
</script>

<style>
body {
  background-color: #ecf0f1;
  background-image: linear-gradient(145deg, rgba(0,0,0,0), rgba(0,0,0,.25));
}

.main {
  margin: 20px;
  align-items: flex-start;
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 15px;
}

@media screen and (max-width: 1200px) {
  .main {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media screen and (max-width: 900px) {
  .main {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media screen and (max-width: 600px) {
  .main {
    grid-template-columns: repeat(1, 1fr);
  }
}

.candidate {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.candidate-logo {
  width: 100px;
  height: 100px;
  margin: 10px;
  background-size: contain;
  border-radius: 50%;
  border: solid 2px black;
}

.name {
  margin: 10px;
  position: relative;
  align-self: flex-start;
}

.tw-logo {
  position: relative;
}

.tw-logo::after {
  content: '';
  display: block;
  background-image: url('../assets/tw-logo.jpg');
  background-size: cover;
  background-position: center;
  width: 25px;
  top: 10px;
  left: -10px;
  height: 25px;
  border-radius: 50%;
  position: absolute;
  margin-left: 10px;
}

.title {
  font-size: 5em;
  text-align: center;
  margin: 1em;
}

.news {
  border: solid 1px #bdc3c7;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  margin-bottom: 15px;
  padding: 10px;
  box-shadow: 0px 0px 15px 1px #bdc3c7;
}

.description {
  text-align: justify;
}

.news-link {
  text-decoration: none;
  color: white;
  background: #7f8c8d;
  padding: 10px;
  margin: 5px;
  transition: background-color .5s, color .5s, border-color .5s;
  border-radius: 25px;
  text-align: center;
}

.news-link:hover {
  background: transparent;
  color: black;
  border: solid 1px black;
}

footer {
  text-align: center;
  margin: 10px;
}

footer a {
  text-decoration: none;
}

.name-twitter-container {
  align-self: center;
  display: flex;
}
</style>
