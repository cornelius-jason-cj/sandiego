<template>
  <main>
    <section class="landing">
      <v-row>
          <v-col cols="12" sm="6" md="6">
            <v-img
              class="logo"
              max-width="240"
            ></v-img>
          </v-col>

          <v-col cols="12" sm="6" md="6">
            <ul class="nav-links">
              <li>About</li>
              <li>Contact</li>
              <li>Location</li>
              <li><v-icon color="#006C5D">mdi-format-list-bulleted</v-icon></li>
            </ul>
          </v-col>
      </v-row>
      

      <v-row>
        <v-col col="12" sm="4" md="4">
          <div class="big-text">
            <h2>Sandiego Hills</h2>
            <span class="small-text">Memorial Park</span>
            <br>
            <span class="detail-text">"Place for someone who give you so much to remember" </span>
            <br>
            <v-btn
              x-large
              color="#006C5D"
              dark
            >
              Contact Us
            </v-btn>
          </div>
        </v-col>

        <v-col col="12" sm="7" md="7" class="carousel-section">
          <v-row>
            <v-col col="12" sm="12" md="12">
              <v-img
                max-height="600"
                :src="this.imgShow"
              ></v-img>
            </v-col>
          </v-row>
          <v-row>
            <v-col
              col="12"
              sm="3"
              md="3"
              v-for="(item,i) in items"
              :key="i"
            >
              <v-card
                class="mx-auto"
                max-width="344"
                height="200"
                @click="changeImage(item)"
              >
                <v-card-text>
                  <p class="display-1 text--primary">
                    {{item.title}}
                  </p>
                  <div class="text--primary">
                    {{item.detail}}
                  </div>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-col>
      </v-row>

    </section>

    <div class="intro">
      <div class="intro-text">
        <h1 class="hide">
          <span class="text">
            Giving The Best Thing
          </span>
        </h1>

        <h1 class="hide">
          <span class="text">
            For Your Lovely
          </span>
        </h1>

        <h1 class="hide">
          <span class="text">
            One
          </span>
        </h1>
      </div>
    </div>

    <div class="slider">

    </div>
  </main>
</template>

<script>

import gsap from "gsap";

export default {
  data () {
    return {
    }
  },
  mounted(){
    this.$nextTick(()=>{ this.animation() });
  },
  methods: {
    animation() {
    },

    changeImage(item) {
      console.log(item)
      this.imgShow = require(`../assets/produk${item.id}.jpg`)
    }
  }
};

</script>


<style scoped>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* 
#FFEFCA 
#D3D4A8
#A5BA8C
#74A077
#3E8768
#006C5D
#2F4858
#887456
*/

</style>