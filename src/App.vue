<template>
  <v-app>
    <v-main
      v-if="$vuetify.breakpoint.width <= 1024"
    >
      <Mobile/>
    </v-main>

    <v-main
      v-else
    >
      <Desktop/>
    </v-main>
  </v-app>
</template>

<script>
import Mobile from './components/Mobile';
import Desktop from './components/Desktop';

export default {
  name: 'App',

  components: {
    Mobile,
    Desktop
  },

  data: () => ({
    //
  }),
};
</script>
