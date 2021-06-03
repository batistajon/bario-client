<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom"  id="baseBar">
        <ion-tab-button id="tab1Button" tab="tab1" href="/tabs/tab1">
          <ion-icon :icon="cafeOutline" />
          <ion-label>Cafés Especiais</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon :icon="cubeOutline" />
          <ion-label>Assinatura</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon :icon="bagHandleOutline" />
          <ion-label>Kits</ion-label>
        </ion-tab-button>
        
        <ion-tab-button tab="ta43" href="/tabs/tab4">
          <ion-icon :icon="beakerOutline" />
          <ion-label>Utensilios</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { cafeOutline, cartOutline, cubeOutline, beakerOutline, bagHandleOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      cafeOutline, 
      cartOutline,
      cubeOutline,
      beakerOutline,
      bagHandleOutline
    }
  }
}
</script>

<style scoped>
ion-page{
  background: #EFC69B;
}
</style>