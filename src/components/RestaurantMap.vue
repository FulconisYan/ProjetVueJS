<template>
    <div> <GmapMap
  :center="{lat: longitude, lng: latitude}"
  :zoom="20"
  map-type-id="terrain"
  style="width: 500px; height: 300px"
>
  <GmapMarker
    :key="index"
    v-for="(m, index) in markers"
    :position="m.position"
    :clickable="true"
    :draggable="true"
    @click="center=m.position"
  />
</GmapMap> </div>
</template>

<script>
    export default {
        name:"Map",
        props: {latitude : Number, longitude : Number},
        data: function() {
    return {
    };
  },
     }
</script>