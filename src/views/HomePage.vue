<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Info Crypto</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-refresher slot="fixed" @ionRefresh="refresh($event)">
        <ion-refresher-content></ion-refresher-content>
      </ion-refresher>

      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Info Crypto</ion-title>
        </ion-toolbar>
      </ion-header>

      <ion-list>
        <CryptoListItem v-for="crypto in cryptos" :key="crypto.id" :crypto="crypto" />
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import {
  IonContent,
  IonHeader,
  IonList,
  IonPage,
  IonRefresher,
  IonRefresherContent,
  IonTitle,
  IonToolbar,
} from '@ionic/vue';
import { ref, onMounted } from 'vue';
import { Crypto } from '@/data/cryptos';
import EndPointAccess from '@/services/EndPointAccess';
import CryptoListItem from '@/components/CryptoListItem.vue';

const cryptos = ref<Crypto[]>([])

const ambilData = async () => {
  const resData = new EndPointAccess('https://api.coinlore.net/api/tickers/');
  const response = await resData.getRes();
  cryptos.value = response.data.data;
  console.log(response.data.data,'cryptos')
};

const refresh = (ev: CustomEvent) => {
  setTimeout(() => {
    ambilData();
    ev.detail.complete();
  }, 1000);
};

onMounted(() => {
  ambilData();
});

</script>