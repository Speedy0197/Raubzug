<template>
  <v-app>
    <v-app-bar
      app
      color="brown"
      dark
    >
      <v-spacer></v-spacer>
        <h2> Raubzug-Rechner </h2>


      <v-spacer></v-spacer>

      
    </v-app-bar>

    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
