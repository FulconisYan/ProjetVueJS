
<template>

<div>
<br/>
<div style="display:flex">
  <img width="400px" style="margin-left: 200px" v-bind:src="image"/>
  <restaurant-map :latitude="latitude" :longitude="longitude"/>
  <br/> <br/> <br/>
</div>
  <h1>Detail du restaurant d'id = {{id}}</h1>
  <p> Adresse : {{address}} </p>
  <p> Description de quartier : {{descrQuartier}} </p>
  <p> Longitude : {{longitude}} </p>
  <p> Latitude : {{latitude}} </p>
  <restaurant-evaluation :grade="grade"/>
  <restaurant-liste />
  
  </div>

</template>

<script>

import RestaurantEvaluation from './RestaurantEvaluation';
import RestaurantListe from './RestaurantListe';
import RestaurantMap from './RestaurantMap';

export default {

  name: "RestaurantDetail",
  props: {},
  components : {
    RestaurantEvaluation,
    RestaurantListe,
    RestaurantMap
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
      latitude:0,
      longitude:0,
      grade:"",
      restaurant:"",
      nom: "",
      address:"",
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
          this.latitude= reponseJS["restaurant"]["address"]["coord"][0]
          this.longitude = reponseJS["restaurant"]["address"]["coord"][1]
          this.grade = reponseJS["restaurant"]["grades"]
          this.menu = reponseJS["menu"]
          this.image = reponseJS["restaurant"]["image"]
        });
    },
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
