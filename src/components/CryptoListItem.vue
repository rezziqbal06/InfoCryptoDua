<template>
  <ion-item v-if="crypto"  class="list-item" :routerLink="'/crypto/'+crypto.id">
    <ion-card>
      <ion-card-content>
        <ion-grid>
          <ion-row>
            <ion-col><small>Rank</small></ion-col>
            <ion-col><small>{{crypto.name}}</small></ion-col>
            <ion-col><small>USD</small></ion-col>
          </ion-row>
          <ion-row>
            <ion-col><h2>{{ crypto.rank }}</h2></ion-col>
            <ion-col><h2>{{crypto.symbol}}</h2></ion-col>
            <ion-col><h2>{{crypto.price_usd}}</h2></ion-col>
          </ion-row>
        </ion-grid>
      </ion-card-content>
    </ion-card>
  </ion-item>
</template>

<script setup lang="ts">
import { IonItem, IonCard, IonCardContent, IonGrid, IonRow, IonCol } from '@ionic/vue';

defineProps({
  crypto: Object,
});


</script>

<style scoped>
ion-card {
  width: 100%;
  background-color: antiquewhite;
  border: 1px solid orange;
}
.list-item {
  --padding-start: 0;
  --inner-padding-end: 0;
}

.list-item ion-label {
  margin-top: 12px;
  margin-bottom: 12px;
}

.list-item h2 {
  font-weight: 600;
  margin: 0;
  
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

.list-item p {
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  width: 95%;
}

.list-item .date {
  align-items: center;
  display: flex;
}

.list-item ion-icon {
  color: #c9c9ca;
}

.list-item ion-note {
  font-size: 0.9375rem;
  margin-right: 8px;
  font-weight: normal;
}

.list-item ion-note.md {
  margin-right: 14px;
}

.list-item .dot {
  display: block;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  align-self: start;
  margin: 16px 10px 16px 16px;
}

.list-item .dot-unread {
  background: red;
}
</style>
