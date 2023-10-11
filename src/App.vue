<template>
  <v-container>
    <v-app id="app">
      <AppHeader class="my-3"></AppHeader>
      <v-main>
        <v-card class="p-3">
          <!-- custom component views -->
          <router-view></router-view>
        </v-card>
      </v-main>
      <v-footer class="my-3 rounded elevation-1">
        <AppFooter></AppFooter>
      </v-footer>
    </v-app>
  </v-container>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';
import AppHeader from './components/AppHeader.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  components: {
    AppHeader,
    AppFooter
  },
};
</script>

<style>
#app {
  background-color: #d8f3dc;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
}
</style>
