<template>
  <v-app>
    <v-content>
      <Frame/>
    </v-content>
  </v-app>
</template>

<script>
import Frame from './components/Frame';

export default {
  name: 'App',

  components: {
    Frame,
  },

  data: () => ({
    //
  }),
};
</script>
