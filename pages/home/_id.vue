<template>
  <div v-if="house">
    <v-container>
      <div class="row">
        <div class="col-md-5 col-sm-5 col-xs-12">
          <v-img
              src='https://cdn.vuetifyjs.com/images/cards/house.jpg'
              height="125"
              class="grey darken-4"
            ></v-img>
            <div class="pl-6 col-6">
            <h2 class="mb-4">{{house.attributes.title}}</h2>
            <p> <b>Etat:</b> Refait à neuf </p>
          </div>
        </div>
        <div class="col-md-7 col-sm-7 col-xs-12 row">
          <div class="col-sm-12 col-xs-12 col-md-12">
            <v-tabs>
              <v-tab >Description</v-tab>
              <v-tab-item>
                <p class="pt-10 subtitle-1 font-weight-thin">
                  {{ house.attributes.description }}
                </p>
              </v-tab-item>
            </v-tabs>
            
          <v-btn
            class="primary white--text col-6 mt-12"
            outlined
            tile
            dense
          >
            Réserver
          </v-btn>
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
        house: null,
      }
    },
    methods: {

    },
    async mounted () {
      const res = (await axios
        .get(`http://localhost:1337/api/houses/${this.$route.params.id}`)).data.data;
        this.house = res;
    }
  }
</script>
