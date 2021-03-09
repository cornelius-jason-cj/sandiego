<template>
  <main>
    <section class="landing">
      <!-- <v-row>
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
       -->

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

        <v-col col="12" sm="8" md="8" class="carousel-section">
          <v-row style="margin-top:40px">
            <v-col col="12" md="11">
              <div v-if="showData">
                <v-row>
                  <v-col cold=12 md="9">
                    <div v-if="this.showDetails === 'Gallery'">
                      <v-row>
                        <v-col
                          v-for="(image,i) in data.images"
                          :key="i"
                          class="d-flex child-flex"
                          cols="3"
                        >
                          <v-img
                            :src="image.src"
                            aspext-ratio="1"
                            class="grey lighten-2"
                          ></v-img>
                        </v-col>
                      </v-row>
                    </div>


                    <div v-else-if="this.showDetails === 'Details'"></div>
                    <div v-else-if="this.showDetails === 'Booking'"></div>
                    <div v-else-if="this.showDetails === 'Maps'"></div>


                    <div v-else>
                      <v-row>
                        <v-col
                          v-for="(image,i) in data.images"
                          :key="i"
                          class="d-flex child-flex"
                          cols="3"
                        >
                          <v-img
                            :src="image.src"
                            class="grey lighten-2"
                          ></v-img>
                        </v-col>
                      </v-row>
                    </div>

                  </v-col>
                  <v-col cold=12 md="3">
                    <v-card
                      class="mx-auto"
                      height="560"
                      color="#887456"
                      elevation="0"
                    >
                      <v-list rounded color="#887456">
                        <v-subheader style="font-size:18px; font-weight:bold; color:#FFEFCA">{{data.title}}</v-subheader>
                        <v-list-item-group
                          v-model="selectedItem"
                          color="#FFEFCA"
                        >
                          <v-list-item
                            v-for="(item, i) in items"
                            :key="i"
                            @click="showDetailType(item.text)"
                          >
                            <v-list-item-icon>
                              <v-icon v-text="item.icon"></v-icon>
                            </v-list-item-icon>
                            <v-list-item-content>
                              <v-list-item-title v-text="item.text"></v-list-item-title>
                            </v-list-item-content>
                          </v-list-item>
                        </v-list-item-group>
                      </v-list>
                    </v-card>
                  </v-col>
                </v-row>
              </div>
              <div v-else>
                <v-img
                  :src="this.imgShow"
                  height="560"
                ></v-img>
              </div>
            </v-col>
            <v-col col="12" md="1"></v-col>
          </v-row>
          <v-row>
            <v-col col="12" md="1"></v-col>
          
            <v-col col="12" md="10">
              <carousel-3d>
                <slide
                  v-for="(slide,i) in cards"
                  :index="i"
                  :key="slide.id"
                >
                  <template slot-scope="{index, isCurrent, leftIndex, rightIndex}" >
                    <v-card @click="openCard(slide.id)" height="100%">
                    <img
                      :data-index="index"
                      :class="{current: isCurrent, onLeft: (leftIndex >= 0), onRight: (rightIndex >= 0)}"
                      :src="slide.src"
                      height="200"
                    />
                    <v-card-title>{{slide.title}}</v-card-title>
                    </v-card>
                  </template>
                </slide>
              </carousel-3d>
            </v-col>
            <v-col col="12" md="1"></v-col>
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
import { Carousel3d, Slide } from 'vue-carousel-3d';

export default {
  data:() => ({
    imgShow: require('../assets/backgroundSandiego.jpg'),
    cards: [
        { id:1, title: 'Promo-Paket Pasangan', text: 'Pembelian 2 unit lahan makam berdampingan', src: require('@/assets/pasangan.png'), flex: 12 },
        { id:2, title: 'Promo-Paket Family', text: 'Pembelian 10 unit lahan makam dalam 1 mansion', src: require('@/assets/family.png'), flex: 12 },
        { id:3, title: 'Tipe Single', subtitle: 'Tipe makam tanpa pembatas kanan dan kirinya', text: 'Luas tanah 1.1m x 3m dan 1.5m x 3m', src: require('@/assets/single.png'), flex: 12 },
        { id:4, title: 'Tipe Semi Private', subtitle: 'Tipe makam yang dapat di isi 2 tipe single dan antar unit dibatasi dengan pembatas tembok atau tanaman', text: 'Luas Tanah 13 - 20.7m2', src: require('@/assets/semiprivate.png'), flex: 12 },
        { id:5, title: 'Tipe Private', subtitle: 'Tipe makam yang dapat di isi 2 - 10 tipe single dan antar unit dibatasi dengan pembatas tembok atau tanaman', text: 'Luas Tanah 25.4 - 180m2', src: require('@/assets/private.png'), flex: 12 },
        { id:6, title: 'Tipe Peak', subtitle: 'Tipe makam paling eksklusif, bisa membangun gazebo dan aksesoris makam seperti patung dan bangku', text: 'Luas Tanah 40 - 222m2', src: require('@/assets/peak.png'), flex: 12 },
      ],
    cardData: [
        {
          id:1,
          images:[
            {
              src: require('@/assets/pasangan.png')
            },
            {
              src: require('@/assets/family.png')
            },
            {
              src: require('@/assets/single.png')
            },
            {
              src: require('@/assets/peak.png')
            },
          ],
          title:'Promo Paket Pasangan',
          text:'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout.'
        },
        {
          id:2,
          images:[
            {
              src: require('@/assets/pasangan.png')
            },
            {
              src: require('@/assets/family.png')
            },
            {
              src: require('@/assets/single.png')
            },
            {
              src: require('@/assets/peak.png')
            },
          ],
          title:'Promo Paket Family',
          text:'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout.'
        },
        {id:3},
        {id:4},
        {id:5},
        {id:6},
      ],
      showData:false,
      data:[],
      selectedItem:0,
      items:[
        { text: 'Gallery', icon: 'mdi-panorama'},
        { text: 'Details', icon: 'mdi-details'},
        { text: 'Booking', icon: 'mdi-book-open'},
        { text: 'Maps', icon: 'mdi-google-maps'},
      ],
      showDetails:''
  }),
  components: {
    Carousel3d,
    Slide
  },
  mounted(){
    this.$nextTick(()=>{ this.animation() });
  },
  methods: {
      animation() {
      const tl = gsap.timeline({ defaults: {ease: "power1.out" }})
      tl.to(".text", { y: "0%", duration: 1.5, stagger: 0.3 });
      tl.to(".slider", {y: "-100%", duration: 1.5, delay: 0.5 });
      tl.to(".intro",{ y: "-100%", duration: 1 }, "-=1");
      tl.fromTo(".nav-links",{ opacity: 0}, { opacity: 1, duration: 1 });

      tl.fromTo(".big-text",{ opacity: 0}, { opacity: 1, duration: 2 }, "");
      tl.fromTo(".small-text",{ opacity: 0}, { opacity: 1, duration: 1 }, "-=2");
      tl.fromTo(".detail-text",{ opacity: 0}, { opacity: 1, duration: 1 });
      tl.fromTo(".carousel-section",{ opacity: 0}, { opacity: 1, duration: 1 });
    },
    changeImage(item) {
      console.log(item)
    },
    openCard(cardId) {
      this.data = this.cardData.find(card => card.id === cardId)
      this.showData = true
      console.log(this.data)
    },
    showDetailType(buttonName) {
      console.log(buttonName)
      this.showDetails=buttonName
      console.log(this.showDetails)
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

.landing {
  min-height: 100vh;
  /* Permalink - use to edit and share this gradient: https://colorzilla.com/gradient-editor/#D4B974+0#D4B974+60,8f754f+60,8f754f+100 */
  background: #FFEFCA; /* Old browsers */
  background: -moz-linear-gradient(left,  #FFEFCA 0%, #FFEFCA 30%, #887456 30%, #887456 100%); /* FF3.6-15 */
  background: -webkit-linear-gradient(left,  #FFEFCA 0%,#FFEFCA 30%,#887456 30%,#887456 100%); /* Chrome10-25,Safari5.1-6 */
  background: linear-gradient(to right,  #FFEFCA 0%,#FFEFCA 30%,#887456 30%,#887456 100%); /* W3C, IE10+, FF16+, Chrome26+, Opera12+, Safari7+ */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#FFEFCA', endColorstr='#887456',GradientType=1 ); /* IE6-9 */
}

.logo{
  margin: 0;
}

.nav-links {
  display: flex;
  list-style: none;
  color: #FFEFCA;
  float: right;
  margin-right:20px;
}

.nav-links li {
  padding: 1rem;
  font-size: 1.2rem;
}

.big-text {
  position: absolute;
  top: 30%;
  left: 5%;
  transform: translate(-5%, -30%);
  font-size: 2rem;
  color: #006C5D;
  max-width: 860px;
}

.detail-text {
  font-size: 1rem;
}

.intro {
  background: #FFEFCA;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.slider {
  background: #006C5D;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  transform: translateY(100%);
}

.intro-text {
  color:#006C5D;
  font-size: 3rem;
}

.hide {
  background: #FFEFCA;
  overflow: hidden;
}

.hide span {
  transform: translateY(100%);
  display: inline-block;
}

.carousel-section {
  padding: 0px;
}

.carousel-pemakaman {
  padding: 0 20px;
  margin: auto
}

.detail1-pemakaman {
  padding: 0 0 0 20px;
  margin: 0 auto;
}

.detail2-pemakaman {
  padding: 0;
  margin: 0 auto;
}

.detail3-pemakaman {
  padding: 0 20px 0 0;
  margin: 0 auto;
}
</style>