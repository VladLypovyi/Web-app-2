<template>
  <v-container>
    <v-layout row class="text-xs-center">
      <v-flex xs4 class="grey lighten-4">
        <v-container style="position: relative;top: 13%;" class="text-xs-center">
          <v-card flat>
            <v-card-title primary-title>
              <h4>Login</h4>
            </v-card-title>
            <v-form>
              <v-card-actions>
                <v-btn @click="handleLogin()" primary large block>Login</v-btn>
              </v-card-actions>
            </v-form>
          </v-card>
        </v-container>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import EosService from '@/eosio/EosService';

export default {
  data() {
    return {
      accountName: '',
      privateKey: '',
      eosio: null
    };
  },
  methods: {
    handleLogin: async function() {
      if (this.eosio === null) {
        this.eosio = new EosService(
          process.env.VUE_APP_DAPP_NAME,
          process.env.VUE_APP_SMART_CONTRACT_NAME
        );
      }

      if (!(await this.eosio.connect()))
        return console.log('Failed to get Scatter account');

      this.$store.commit('loginStatus', true);
      this.$router.push('start'); //home
      console.log('login');

      /*if (
        await this.eosio.transaction('login', { user: this.eosio.account.name })
      ) {
        this.$store.commit('loginStatus', true);
        this.$router.push('home');
        return console.log('login');
      }*/
    }
  }
};
</script>
