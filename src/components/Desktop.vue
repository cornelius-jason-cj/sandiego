<template>
  <div></div>
</template>

<script>
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