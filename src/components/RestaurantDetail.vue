<template>
<div>
  <h1>Detail du restaurant d'id = {{id}}</h1>
  <p> Adresse : {{address}} </p>
  <p> Description de quartier : {{descrQuartier}} </p>
  <p> Longitude : {{longitude}} </p>
  <p> Latitude : {{latitude}} </p>
  <p> Notes des utilisateurs : {{note1}}  {{note2}}  {{note3}}  {{note4}} </p>
  </div>
</template>

<script>
export default {
  name: "RestaurantDetail",
  props: {},
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
          console.log(reponseJS)
          this.address = reponseJS["restaurant"]["address"]["building"] + " "+ reponseJS["restaurant"]["address"]["street"]
          this.descrQuartier = reponseJS["restaurant"]["borough"]
          this.longitude = reponseJS["restaurant"]["address"]["coord"][0]
          this.latitude = reponseJS["restaurant"]["address"]["coord"][1]
          this.note1 = reponseJS["restaurant"]["grades"][0]["grade"]+","
          this.note2 = reponseJS["restaurant"]["grades"][1]["grade"]+","
          this.note3 = reponseJS["restaurant"]["grades"][2]["grade"]+","
          this.note4 = reponseJS["restaurant"]["grades"][3]["grade"]
          
          
        });
    },
    
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
