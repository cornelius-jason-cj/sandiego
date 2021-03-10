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
        <v-col col="12" md="3">
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

        <v-col col="12" md="9" class="carousel-section">
          <v-row style="margin-top:40px">
            <v-col col="12" md="12">
              <div v-if="showData">
                <v-row style="margin:0 40px 40px 40px">
                  <v-col cols="12" md="12">
                    <v-card
                      height="560"
                    >
                      <v-toolbar
                        flat
                        color="#006C5D"
                        dark
                      >
                        <v-toolbar-title>{{this.data.title}}</v-toolbar-title>
                      </v-toolbar>
                      <v-tabs
                        vertical
                        background-color="#006C5D"
                        color="#FFEFCA"  
                      >
                        <v-tab>
                          Universal
                        </v-tab>

                        <v-tab>
                          Muslim
                        </v-tab>

                        <v-tab>
                          Chinese
                        </v-tab>

                        <v-tab-item>
                          <v-card flat>
                            <v-container fluid>
                              <v-data-iterator
                                :items="items"
                                :items-per-page.sync="itemsPerPage"
                                :page.sync="page"
                                :search="search"
                                :sort-by="sortBy.toLowerCase()"
                                :sort-desc="sortDesc"
                                hide-default-footer
                                style="background-color:#FFEFCA"
                              >
                                <template v-slot:header>
                                  <v-toolbar
                                    dark
                                    color="#006C5D"
                                    class="mb-1"
                                  >
                                    <v-text-field
                                      v-model="search"
                                      clearable
                                      flat
                                      solo-inverted
                                      hide-details
                                      prepend-inner-icon="mdi-magnify"
                                      label="Search"
                                    >
                                    </v-text-field>
                                    <template v-if="$vuetify.breakpoint.mdAndUp">
                                      <v-spacer></v-spacer>
                                      <v-select
                                        v-model="sortBy"
                                        flat
                                        solo-inverted
                                        hide-details
                                        :items="keys"
                                        prepend-inner-icon="mdi-magnify"
                                        label="Sort by"
                                      ></v-select>
                                      <v-spacer></v-spacer>
                                      <v-btn-toggle
                                        v-model="sortDesc"
                                        mandatory
                                      >
                                        <v-btn
                                          depressed
                                          color="#006C5D"
                                          :value="false"
                                        >
                                          <v-icon>mdi-arrow-up</v-icon>
                                        </v-btn>

                                        <v-btn
                                          depressed
                                          color="#006C5D"
                                          :value="true"
                                        >
                                          <v-icon>mdi-arrow-down</v-icon>
                                        </v-btn>
                                      </v-btn-toggle>
                                    </template>
                                  </v-toolbar>
                                </template>

                                <template v-slot:default="props">
                                  <v-row style="margin-left:8px">
                                    <v-col
                                      v-for="item in props.items"
                                      :key="item.id"
                                      cols="12"
                                      md="3"
                                    >
                                      <v-card width="300" height="420" style="margin: 4px 0">
                                        <v-card-title class="subheading font-weight-bold">
                                          {{ item.mansion }}
                                        </v-card-title>

                                        <v-divider></v-divider>
                                        <v-img
                                          :src="item.src"
                                        />

                                        <v-list dense>
                                          <v-list-item
                                            v-for="(key, index) in filteredKeys"
                                            :key="index"
                                          >
                                            <v-list-item-content :class="{ 'green--text': sortBy === key}">
                                              {{ key }}:
                                            </v-list-item-content>
                                            <v-list-item-content
                                              class="align-end"
                                              :class="{ 'green--text': sortBy === key }"
                                            >
                                              {{ item[key.toLowerCase()]}}
                                            </v-list-item-content>
                                          </v-list-item>
                                        </v-list>
                                      </v-card>
                                    </v-col>
                                  </v-row>
                                </template>

                                <template v-slot:footer>
                                  <v-row
                                    class="mt-2"
                                    align="center"
                                    justify="center"
                                  >
                                    <span class="grey--text">Items per page</span>
                                    <v-menu offset-y>
                                      <template v-slot:activator="{ on, attrs }">
                                        <v-btn
                                          dark
                                          text
                                          color="primary"
                                          v-bind="attrs"
                                          v-on="on"
                                        >
                                          {{ itemsPerPage }}
                                          <v-icon>mdi-chevron-down</v-icon>
                                        </v-btn>
                                      </template>

                                      <v-list>
                                        <v-list-item
                                          v-for="(number, index) in itemsPerPageArray"
                                          :key="index"
                                          @click="updateItemsPerPage(number)"
                                        >
                                          <v-list-item-title>{{ number }}</v-list-item-title>
                                        </v-list-item>
                                      </v-list>
                                    </v-menu>

                                    <v-spacer></v-spacer>

                                    <span
                                      class="mr-4"
                                      grey--text
                                    >
                                      Page {{ page }} of {{ numberOfPages }}
                                    </span>
                                    <v-btn
                                      fab
                                      dark
                                      color="#006C5D"
                                      class="mr-1"
                                      @click="formerPage"
                                      small
                                    >
                                      <v-icon>mdi-chevron-left</v-icon>
                                    </v-btn>

                                    <v-btn
                                      fab
                                      dark
                                      color="#006C5D"
                                      class="ml-1"
                                      @click="nextPage"
                                      small
                                    >
                                      <v-icon>mdi-chevron-right</v-icon>
                                    </v-btn>
                                  </v-row>
                                </template>

                              </v-data-iterator>
                            </v-container>
                          </v-card>
                        </v-tab-item>

                        <v-tab-item>
                          <v-card flat>
                            <v-card-text>
                              <p>harga Muslim</p>
                            </v-card-text>
                          </v-card>
                        </v-tab-item>

                        <v-tab-item>
                          <v-card flat>
                            <v-card-text>
                              <p>harga Chinese</p>
                            </v-card-text>
                          </v-card>
                        </v-tab-item>
                      </v-tabs>
                    </v-card>
                  </v-col>
                </v-row>
              </div>
              <div v-else>
                <v-img
                  :src="this.imgShow"
                  height="600"
                  max-width="1320"
                  style="margin-left:40px"
                ></v-img>
              </div>
            </v-col>
            <v-col col="12" md="1"></v-col>
          </v-row>
          <v-row>
            <v-col col="12" md="12">
              <carousel-3d>
                <slide
                  v-for="(slide,i) in cards"
                  :index="i"
                  :key="slide.id"
                  style="border-radius: 10px"
                >
                  <template slot-scope="{index, isCurrent, leftIndex, rightIndex}" >
                    <v-card @click="openCard(slide.id)" height="100%" class="cardSlideCarousel">
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
          id: 1,
          images: [
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
          title: 'Promo Paket Pasangan',
          text: 'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout.'
        },
        {
          id: 2,
          images: [
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
          title: 'Promo Paket Family',
          text: 'It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout.'
        },
        {id: 3},
        {id: 4},
        {id: 5},
        {id: 6},
      ],
      showData: false,
      data: [],
      showDetails: '',
      itemsPerPageArray: [4,8,12],
      search: '',
      filter: {},
      sortDesc: false,
      page: 1,
      itemsPerPage: 4,
      sortBy: 'Mansion',
      keys: [
        'Mansion',
        'Pembayaran',
        'Harga',
        'Ukuran',
      ],
      items: [
        {
          id:1,
          mansion: 'Serenity-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cicil',
          harga: 'Rp 63.476.600',
          ukuran: '1.1m x 3m',
          src:require('@/assets/single.png')
        },
        {
          id:2,
          mansion: 'Serenity-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cash',
          harga: 'Rp 57.128.940',
          ukuran: '1.1m x 3m',
          src:require('@/assets/single.png')
        },
        {
          id:3,
          mansion: 'Serenity-Pasangan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cicil',
          harga: 'Rp 110.000.000',
          ukuran: '1.1m x 3m',
          src:require('@/assets/pasangan.png')
        },
        {
          id:4,
          mansion: 'Serenity-Pasangan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cash',
          harga: 'Rp 99.000.000',
          ukuran: '1.1m x 1.3',
          src:require('@/assets/pasangan.png')
        },
        {
          id:5,
          mansion: 'Grace-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cicil',
          harga: 'Rp 63.476.600',
          ukuran: '1.1m x 3m',
          src:require('@/assets/family.png')
        },
        {
          id:6,
          mansion: 'Grace-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cash',
          harga: 'Rp 57.128.940',
          ukuran: '1.1m x 3m',
          src:require('@/assets/family.png')
        },
        {
          id:7,
          mansion: 'Grace-Pasangan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cicil',
          harga: 'Rp 110.000.000',
          ukuran: '1.1m x 3m',
          src:require('@/assets/private.png')
        },
        {
          id:8,
          mansion: 'Grace-Pasangan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cash',
          harga: 'Rp 99.000.000',
          ukuran: '1.1m x 3m',
          src:require('@/assets/private.png')
        },
        {
          id:9,
          mansion: 'Serenity New-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cicil',
          harga: 'Rp 101.750.000',
          ukuran: '1.5m x 3m',
          src:require('@/assets/peak.png')
        },
        {
          id:10,
          mansion: 'Serenity New-Single',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Single',
          pembayaran: 'Cash',
          harga: 'Rp 91.575.000',
          ukuran: '1.5m x 3m',
          src:require('@/assets/peak.png')
        },
        {
          id:11,
          mansion: 'Serenity New-Pasnagan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cicil',
          harga: 'Rp 185.000.000',
          ukuran: '1.5m x 3m',
          src:require('@/assets/semiprivate.png')
        },
        {
          id:12,
          mansion: 'Serenity New-Pasangan',
          nuansa: 'Kristen/Katolik/Buddha',
          tipe: 'Pasangan',
          pembayaran: 'Cash',
          harga: 'Rp 166.500.000',
          ukuran: '1.5m x 1.3',
          src:require('@/assets/semiprivate.png')
        },
      ]
  }),
  components: {
    Carousel3d,
    Slide
  },
  mounted(){
    this.$nextTick(()=>{ this.animation() });
  },
  computed: {
    numberOfPages () {
      return Math.ceil(this.items.length / this.itemsPerPage)
    },
    filteredKeys () {
      return this.keys.filter(key => key !== 'Mansion')
    }
  },
  methods: {
      animation () {
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
    changeImage( item) {
      console.log(item)
    },
    openCard (cardId) {
      this.data = this.cardData.find(card => card.id === cardId)
      this.showData = true
      console.log(this.data)
    },
    nextPage () {
      if (this.page + 1 <= this.numberOfPages) this.page += 1
    },
    formerPage () {
      if (this.page -1 >= 1) this.page -= 1
    },
    updateItemsPerPage (number) {
      this.itemsPerPage = number
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

.cardSlideCarousel{
  padding: 4px;
  border-radius: 10px;
}

.slide-fade-enter-active {
  transition: all 5s ease;
}
.slide-fade-leave-active {
  transition: all 1s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
</style>