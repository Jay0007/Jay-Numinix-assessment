<template>
  <v-app style="font-family: Rubik">
    <v-app-bar
      height = "91px"
      app
      color="#FFFFFF"
      style="box-shadow: 9px 6px 24px -2px rgba(0, 0, 0, 0.06);"
    >
    </v-app-bar>

    <v-main style="background: #F2F5FA;">
      <Home/>
    </v-main>
  </v-app>
</template>

<script>
import Home from './components/Home';

export default {
  name: 'App',

  components: {
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
