<template>
  <v-app>
    <v-app-bar color="green" dense dark app>
      <v-toolbar-title>回文数計算</v-toolbar-title>
    </v-app-bar>
    <v-main>
      <Calculate/>
    </v-main>
  </v-app>
</template>

<script>
import Calculate from './components/Calculate';

export default {
  name: 'App',

  components: {
    Calculate,
  },

  data: () => ({
    //
  }),
};
</script>
