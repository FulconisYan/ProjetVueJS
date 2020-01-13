<template>
    <div> 
        <br/>
        <h1> Menus et plats </h1>
        <br/>
        <div style="display: flex">
        <div style="text-align: left; margin-left:200px">
            <p> Menu Gastronomique </p>
        </div>
        <div style="text-align: center; margin-left:575px; margin-right:200px;">
            <p> Menu Simple </p>
        </div>
        <div style="text-align: right; margin-right:200px; margin-left:200px;">
            <p> Menu Special </p>
        </div>
        </div>

        <div style="display: inline-block;">
        <v-container>
            <v-flex xs12 md6>
                <v-data-table
    style = "width : 500px;"
    :headers="headers"
    :items="entrees"
    :items-per-page="5"
    group-by="categorie"
  ></v-data-table>
  </v-flex>
  </v-container>
     </div>
  <div style="display:flex; justify-content : space-around">
  <div class="my-2">
        <v-btn color="primary">Choisir</v-btn>
      </div>
      <div class="my-2">
        <v-btn color="primary">Choisir</v-btn>
      </div>
      <div class="my-2">
        <v-btn color="primary">Choisir</v-btn>
      </div>
    </div>
    </div>
  
</template>

<script>
    export default {
       name:"Menu",
       props: {menu: Array},
       data () {
    return {
      headers: [
        {
          text: "MenuSimple",
          align: 'left',
          value: 'name',
        },
        { text: 'Categorie', value: 'categorie' },
      ],
      entrees: [
        {
          name: 'Frozen Yogurt',
          categorie: 'Entree',
        },
        {
          name: 'Ice cream sandwich',
          categorie: 'Entree',
        },
        {
          name: 'Eclair',
          categorie: 'Entree',
        },
        {
          name: 'Cupcake',
          categorie: 'Entree',
        },
        {
          name: 'Gingerbread',
          categorie: 'Entree',
        },
        {
          name: 'Jelly bean',
          categorie: 'Entree',
        },
        {
          name: 'Lollipop',
          categorie: 'Plats',
        },
        {
          name: 'Honeycomb',
          categorie: 'Desserts',
        },
        {
          name: 'Donut',
          categorie: 'Desserts',
        },
        {
          name: 'KitKat',
          categorie: 'Plats',
        },
      ],
    }
  },
}
</script>