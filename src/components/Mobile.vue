<template>
 <v-container fluid>
      <v-row dense>
        <v-img
          :src="sdhlogo"
        ></v-img>
        <v-col
          v-for="card in cards"
          :key="card.id"
          :cols="card.flex"
        >
          <v-card @click="openCard(card.id)">
            <v-img
              :src="card.src"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="200px"
            >
            </v-img>
            <v-card-text>
              <div class="font-weight-bold" v-text="card.title"></div>
              <div v-text="card.subtitle"></div>
              <div v-text="card.text"></div>
            </v-card-text>
          </v-card>
        </v-col>

        <v-dialog
          v-model="dialog"
        >
          <v-card>
            <v-system-bar>
              <v-icon @click="dialog=false">mdi-close</v-icon>
            </v-system-bar>
            <v-carousel
              hide-delimiters
              show-arrows-on-hover
              height="200px"
            >
              <v-carousel-item
                v-for="(item,i) in cardData[0].images"
                :key="i"
                :src="item.src"
              ></v-carousel-item>
            </v-carousel>

            <v-card-action>
              <v-btn
                color="green"
                text
              >
                Whatsapp
              </v-btn>
            </v-card-action>
          </v-card>
        </v-dialog>
      </v-row>
    </v-container>
</template>

<script>
  export default {
    name: 'Mobile',
    data: () => ({
      dialog: false,
      sdhlogo:require('@/assets/sdhlogo.png'),
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
          ]
        },
        {id:2},
        {id:3},
        {id:4},
        {id:5},
        {id:6},
      ],
      data:[]
    }),
    methods: {
      openCard(cardId) {
        this.dialog = true
        this.data = this.cardData.find(card => card.id === cardId)
      }
    }
  }
</script>

<style scoped>
  body{
    background-color: #F6EDD9;
  }

  .card-box{
    padding: 20px 0;
    border-bottom: 1px solid black;
  }
</style>