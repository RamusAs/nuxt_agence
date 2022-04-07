<template>
  <v-container fluid>
      <v-row dense>
        <v-col class="d-flex" >
        
    <v-card  
     v-for="house in houses" :key="house.id"
    class="mx-auto my-12"
    max-width="374"
  >
    <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        indeterminate
      ></v-progress-linear>
    </template>

    <v-img
      height="250"
      src='https://cdn.vuetifyjs.com/images/cards/house.jpg'
    ></v-img>

    <v-card-title>{{house.attributes.title}}</v-card-title>

    <v-card-text>
      <v-row
        align="center"
        class="mx-0"
      >
        <div class="grey--text ms-4">
          {{house.attributes.surface}}m²
        </div>
      </v-row>

      <div class="my-4 text-subtitle-1">
        {{house.attributes.city}}
      </div>

      <div>{{house.attributes.description}}</div>
    </v-card-text>

    <v-divider class="mx-4"></v-divider>

    <v-card-text>
      <v-chip-group column >
        <v-chip>{{house.attributes.price}}€</v-chip>
      </v-chip-group>
    </v-card-text>

    <v-card-actions>
      <NuxtLink :to="`home/${house.id}`">
        <v-btn
        color="deep-purple lighten-2"
        text
        >
          Voir
        </v-btn>
      </NuxtLink>
    </v-card-actions>
  </v-card> 
        </v-col>
      </v-row>
    </v-container>
 </template>


<script>
  import axios from "axios"

  export default {
    name: 'HousesPage',
    data () {
      return {
        houses: {},
      }
    },

  async mounted () {
      this.houses = (await axios
        .get('http://localhost:1337/api/houses')).data.data
    }
    
  }
</script>
