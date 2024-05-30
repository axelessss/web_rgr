<template>
  <div class="currency-widget">
    <div class="header">
      <h2>Курсы криптовалют/USD</h2>
    </div>
    <div class="content">
      <div v-if="loading" class="loading">Загрузка...</div>
      <div v-else>
        <ul class="rates-list">
          <li v-for="(crypto, index) in cryptos" :key="index" class="rate-item">
            <span class="currency">{{ crypto.symbol }}:</span>
            <span class="rate">{{ crypto.priceUsd }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'CurrencyWidget',
  data() {
    return {
      cryptos: [],
      loading: true
    };
  },
   async created() {
    try {
      const response = await axios.get('https://api.coincap.io/v2/assets?ids=bitcoin,ethereum,litecoin,dogecoin,ripple,cardano,polkadot,chainlink,stellar,tezos,usdt');
      this.cryptos = response.data.data;
      this.loading = false;
    } catch (error) {
      console.error('Ошибка при загрузке курсов криптовалют:', error);
    }
  },
};
</script>

<style scoped>
@import '../assets/styles.css';
</style>