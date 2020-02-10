<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h2>Secure ssh-keygen only on Web browser</h2>
      </div>
    </v-app-bar>

    <v-content>
      <SshKeygen/>
    </v-content>

    <v-footer padless color="primary darken-1">
      <v-row justify="center"
             no-gutters>
        <v-col
          class="white py-4 text-center"
          cols="12"
        >
        ❤️ Thanks: The core of this project was originally created by <a href="http://blog.roumanoff.com/">Patrick Roumanoff</a>. Thanks! His repository is found on <a href="https://github.com/PatrickRoumanoff/js-keygen">PatrickRoumanoff/js-keygen</a>.<br>
        The repository of this project is located at <a href="https://github.com/nwtgck/ssh-keygen-web">nwtgck/ssh-keygen-web</a>
      </v-col>
    </v-row>
  </v-footer>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue';
import SshKeygen from './components/SshKeygen.vue';

export default Vue.extend({
  name: 'App',

  components: {
    SshKeygen,
  },

  data: () => ({
    //
  }),
});
</script>
