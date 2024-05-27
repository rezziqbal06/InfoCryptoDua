<template>
    <ion-page>
      <ion-header :translucent="true">
        <ion-toolbar>
          <ion-buttons slot="start">
            <ion-back-button :text="getBackButtonText()" default-href="/"></ion-back-button>
          </ion-buttons>
        </ion-toolbar>
      </ion-header>
  
      <ion-content :fullscreen="true" v-if="crypto">
        <div class="ion-padding">
            <small>Rank {{ crypto.rank }}</small>
        </div>
        <ion-item>
          <ion-label class="ion-text-wrap">
            <h2>
              {{ crypto.name }}
              <span class="date">
                <ion-note>{{ crypto.symbol }}</ion-note>
              </span>
            </h2>
          </ion-label>
        </ion-item>

  
        <div class="ion-padding">
          <h1>$ {{ crypto.price_usd }}</h1>
        </div>

        
        <ion-grid>
          <ion-row>
            <ion-col>1H</ion-col>
            <ion-col>24H</ion-col>
            <ion-col>7D</ion-col>
          </ion-row>
          <ion-row>
            <ion-col><h2><b>{{crypto.percent_change_1h}}%</b></h2></ion-col>
            <ion-col><h2><b>{{crypto.percent_change_24h}}%</b></h2></ion-col>
            <ion-col><h2><b>{{crypto.percent_change_7d}}%</b></h2></ion-col>
          </ion-row>
        </ion-grid>
      </ion-content>
    </ion-page>
  </template>
  
  <script setup lang="ts">
  import { useRoute } from 'vue-router';
  import {
    IonBackButton,
    IonButtons,
    IonContent,
    IonHeader,
    IonItem,
    IonLabel,
    IonNote,
    IonPage,
    IonToolbar,
  } from '@ionic/vue';
  import { ref, onMounted } from 'vue';
  import EndPointAccess from '@/services/EndPointAccess';
  
  const getBackButtonText = () => {
    const win = window as any;
    const mode = win && win.Ionic && win.Ionic.mode;
    return mode === 'ios' ? 'Inbox' : '';
  };
  
  const crypto = ref<Crypto>()

  const route = useRoute();

  const ambilData = async() => {
    const id = parseInt(route.params.id as string, 10);
    const resData = new EndPointAccess('https://api.coinlore.net/api/ticker/?id='+id);
    const response = await resData.getRes();
    crypto.value = response.data[0];
  }


  onMounted(() => {
    ambilData();
  });

  </script>
  
  <style scoped>
  ion-item {
    --inner-padding-end: 0;
    --background: transparent;
  }
  
  ion-label {
    margin-top: 12px;
    margin-bottom: 12px;
  }

	.text-center{
		text-align: center;
	}
  
  ion-item h2 {
    font-weight: 600;
    
    /**
     * With larger font scales
     * the date/time should wrap to the next
     * line. However, there should be
     * space between the name and the date/time
     * if they can appear on the same line.
     */
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  ion-item .date {
    align-items: center;
    display: flex;
  }
  
  ion-item ion-icon {
    font-size: 42px;
    margin-right: 8px;
  }
  
  ion-item ion-note {
    font-size: 0.9375rem;
    margin-right: 12px;
    font-weight: normal;
  }

  ion-grid{
    text-align: center;
  }
  
  h1 {
    margin: 0;
    font-weight: bold;
    font-size: 1.4rem;
  }
  
  p {
    line-height: 1.4;
  }
  </style>
  