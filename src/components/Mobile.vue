<template>
 <v-container fluid>
      <v-row dense>
        <v-img
          :src="sdhlogo"
        ></v-img>
        <v-col
          v-for="card in cards"
          :key="card.title"
          :cols="card.flex"
        >
          <v-card>
            <v-img
              :src="card.src"
              class="white--text align-end"
              gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
              height="200px"
            >
              <v-card-title v-text="card.title"></v-card-title>
              <v-card-text v-text="card.subtitle"></v-card-text>
              <v-card-text v-text="card.text"></v-card-text>
            </v-img>

            <v-card-actions>
              <v-spacer></v-spacer>

              <v-btn icon>
                <v-icon>mdi-heart</v-icon>
              </v-btn>

              <v-btn icon>
                <v-icon>mdi-bookmark</v-icon>
              </v-btn>

              <v-btn icon>
                <v-icon>mdi-share-variant</v-icon>
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
</template>

<script>
  export default {
    name: 'Mobile',
    data: () => ({
      sdhlogo:require('@/assets/sdhlogo.png'),
      cards: [
        { title: 'Promo', subtitle: 'Paket Pasangan', text: 'Pembelian 2 unit lahan makam berdampingan', src: require('@/assets/pasangan.png'), flex: 12 },
        { title: 'Promo', subtitle: 'Paket Family', text: 'Pembelian 10 unit lahan makam dalam 1 mansion', src: require('@/assets/family.png'), flex: 12 },
        { title: 'Tipe Single', subtitle: 'Tipe Makam tanpa pembatas kanan dan kirinya', text: 'Tipe Makam tanpa pembatas kanan dan kirinya', src: require('@/assets/single.png'), flex: 12 },
      ],
    }),
  }
</script>

<style scoped>
  body{
    background-color: #F6EDD9;
  }
</style>