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
