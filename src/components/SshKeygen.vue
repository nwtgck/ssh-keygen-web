<template>
  <v-container>
    <v-row justify="center" class="ma-2">
      <v-radio-group v-model="keySizeStr" row>
        <v-radio label="2048 bits" value="2048"></v-radio>
        <v-radio label="4096 bits" value="4096"></v-radio>
      </v-radio-group>
    </v-row>

     <v-row justify="center" class="ma-2">
      <v-radio-group v-model="hashAlg" row>
        <v-radio label="SHA-256" value="SHA-256"></v-radio>
        <v-radio label="SHA-384" value="SHA-384"></v-radio>
        <v-radio label="SHA-512" value="SHA-512"></v-radio>
      </v-radio-group>
    </v-row>

    <v-row justify="center" class="ma-2">
      <v-text-field v-model="email" label="email (optional)"/>
    </v-row>

    <v-row justify="center" class="ma-2">
      <v-btn color="primary"
             @click="generateKeys()"
             :loading="generatingKeys"
             :disabled="generatingKeys">
        <v-icon left>{{ icons.mdiKey }}</v-icon>
        Generate
      </v-btn>
    </v-row>
    
    <v-row justify="center" v-if='publicKey !== ""'>
      <v-textarea v-model="publicKey" outlined label="Public key" />
    </v-row>

    <v-row justify="center" v-if='privateKey !== ""'>
      <v-textarea v-model="privateKey" outlined label="Private key" />
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import {generateKeyPair} from 'web-ssh-keygen';
import {mdiKey} from "@mdi/js"; 


@Component
export default class SshKeygen extends Vue {
  private keySizeStr: "2048" | "4096" = "4096";
  private hashAlg: "SHA-256" | "SHA-384" | "SHA-512" = "SHA-256";
  private email: string = "" as string;
  private generatingKeys: boolean = false as boolean;
  private publicKey: string = "" as string;
  private privateKey: string = "" as string;

  private icons = {
    mdiKey,
  };

  private async generateKeys(): Promise<void> {
    this.generatingKeys = true;
    const {privateKey, publicKey} = await generateKeyPair({
      alg: "RSASSA-PKCS1-v1_5",
      size: this.keySize,
      hash: this.hashAlg,
      name: this.email,
    });
    this.generatingKeys = false;
    this.publicKey = publicKey;
    this.privateKey = privateKey;
  }

  // eslint-disable-next-line getter-return
  private get keySize(): 2048 | 4096 {
    switch (this.keySizeStr) {
      case "2048":
        return 2048;
      case "4096":
        return 4096;
    }
  }
}
</script>

<style scoped>
</style>
