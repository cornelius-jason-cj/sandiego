<template>
  <v-card
    v-if="$vuetify.breakpoint.width < 414"
  >
    <h1>Mobile</h1>
  </v-card>
  
  <v-card
    v-else
  >
    <h1>Not Mobile</h1>
  </v-card>
</template>

<script>
  export default {
    name: 'HelloWorld',
  }
</script>
