<template>
    <div>  
        Note des utilisateurs :
        <ul id="example-1">
        <li style="list-style-type:none" v-for="item in grade" v-bind:key=item>
            <v-rating
      v-model="rating"
      background-color="indigo lighten-3"
      color="indigo"
      size="64"
      readonly="true"
    ></v-rating>
    {{item["grade"]}}
        </li>
        </ul>
  </div>
  

</template>

<script>
    export default {
        name:"Grades",
        props: {grade: Array},
        data: function() {
        return {
            rating:"3"
        }
         },
         methods: {
         }
     }
</script>
