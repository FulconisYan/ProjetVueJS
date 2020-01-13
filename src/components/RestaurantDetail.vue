
<template>

<div>
<br/>
  <img width="400px" v-bind:src="image"/>
  <br/> <br/> <br/>

  <h1>Detail du restaurant d'id = {{id}}</h1>
  <p> Adresse : {{address}} </p>
  <p> Description de quartier : {{descrQuartier}} </p>
  <p> Longitude : {{longitude}} </p>
  <p> Latitude : {{latitude}} </p>
  <restaurant-evaluation :grade="grade"/>
  <restaurant-liste :menuGastronomiqe="menuGastronomique"/>
  </div>

</template>

<script>

import RestaurantEvaluation from './RestaurantEvaluation';
import RestaurantListe from './RestaurantListe';

export default {

  name: "RestaurantDetail",
  props: {},
  components : {
    RestaurantEvaluation,
    RestaurantListe
  },
  computed: { // computed data, permet de définir des data "calculées"
      id() {
        // on y accèdera par {{id}} dans le template, et par this.id
        // dans le code
      return this.$route.params.id
    }
  },
  data: function() {
    return {
      restaurant:"",
      nom: "",
      address:"",
      longitude:"",
      latitude:"",
      note1:"",
      note2:"",
      note3:"",
      note4:"",
      cuisine: "",
      page: 0,
      pagesize: 10,
      nomRecherche: "",
      image:"",
      nbPagesDeResultats: 0,
      descrQuartier:"",
      apiURL: "http://localhost:8080/api/restaurants/"
    };
  },
  mounted() {
    console.log("AVANT AFFICHAGE !");
    console.log("On va chercher les détails du restaurant id = " + this.$route.params.id)
    console.log("ID = " + this.id);
    this.getDataFromServer();
  },
  methods: {
    getDataFromServer() {
      // ici on fait un fetch pour récupérer le détail du restaurant
      let url =
        this.apiURL +
        this.$route.params.id;
        console.log(url)
        fetch(url)
        .then(reponseJSON => {
          return reponseJSON.json();
        })
        .then(reponseJS => {
          this.address = reponseJS["restaurant"]["address"]["building"] + " "+ reponseJS["restaurant"]["address"]["street"]
          this.descrQuartier = reponseJS["restaurant"]["borough"]
          this.longitude = reponseJS["restaurant"]["address"]["coord"][0]
          this.latitude = reponseJS["restaurant"]["address"]["coord"][1]
          this.grade = reponseJS["restaurant"]["grades"]
          this.menu = reponseJS["menu"]
          this.image = reponseJS["restaurant"]["image"]
          console.log(this.image)
        });
    },
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
