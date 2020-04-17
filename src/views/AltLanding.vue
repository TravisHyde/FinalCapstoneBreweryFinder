<template>
  <v-content align="center" class="altlanding secondary">
    <v-row align="center">
        <v-col
            md=4
            cols="12"
            sm="4">
    <v-card dark class="accent">
        <brewery-search-card></brewery-search-card>
    </v-card>
</v-col>

     <v-col
            md=4
            cols="12"
            sm="4">
    <v-container>
    <v-card>
    <v-carousel height="140px" continuous cycle dark interval="4000" show-arrows show-arrows-on-hover touch>
      <v-carousel-item  v-for="(image, i) in images" :key="i">
        <v-img 
        :src="image"
        
        position="center"
        ></v-img>
      </v-carousel-item>
    </v-carousel>
    </v-card>
    </v-container>
    </v-col>


 <v-col 
            md=4
            cols="12"
            sm="4">
    <v-card dark class="accent">
        <search-beers></search-beers>
    </v-card>
</v-col>

 
</v-row>
  </v-content>
</template>

<script>

import SearchBeers from "@/components/SearchBeers.vue";
import BrewerySearchCard from "@/components/BrewerySearchCard.vue";

export default {
  name: "altlanding",
  data() {
    return {
      breweries: [],
      images: []
    }
  },
  components: {
    SearchBeers,
    BrewerySearchCard
  },
  methods: {
    setImages(){
      this.breweries.forEach(brewery => {
        this.images.push(brewery.imageLocation)
      });
    }
  },
  created() {
    fetch(`${process.env.VUE_APP_REMOTE_API}/breweries`, {
      method: "GET",
      headers: {
        Accept: "application/json",
        "Content-Type": "application/json"
      }
    })
      .then(response => {
        return response.json();
      })
      .then(data => {
        this.breweries = data;
        this.setImages();
      })
      .catch(err => console.error(err));
  }
};
</script>

<style>
</style>