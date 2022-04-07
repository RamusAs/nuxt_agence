<template>
  <div>
    <v-container>
      <div class="row">
        <div class="col-md-5 col-sm-5 col-xs-12">
          <v-img
            :src="house.image"
            aspect-ratio="1"
          >
          </v-img>
        </div>
        <div class="col-md-7 col-sm-7 col-xs-12 row">
          <div class="pl-6 col-6">
            <h2 class="mb-4">{{house.attributes.title}}</h2>
            <p> <b>Etat: </b> </p>
          </div>
          <v-btn
            class="primary white--text col-6 mt-12"
            outlined
            tile
            dense
          >
            <v-icon>mdi-cart</v-icon>
            Réserver
          </v-btn>
          <div class="col-sm-12 col-xs-12 col-md-12">
            <v-tabs>
              <v-tab >Description</v-tab>
              <v-tab-item>
                <p class="pt-10 subtitle-1 font-weight-thin">
                  {{ house.attributes.description }}
                </p>
              </v-tab-item>
            </v-tabs>
          </div>
        </div>
      </div>
    </v-container>
  </div>
</template>
<script>
import axios from "axios";

  export default {
    data () {
      return {
        house: {},
        id: this.$routes.params.id
      }
    },
    methods: {

    },
    async mounted () {
    await axios
      .get(`http://localhost:1337/api/houses/${this.id}`)
      .then(response => {
        this.house = response.data.data;})
    }
  }
</script>
