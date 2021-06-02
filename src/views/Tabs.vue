<template>
  <ion-page>
    <ion-tabs>
      <ion-tab-bar slot="bottom"  id="baseBar">
        <ion-tab-button id="tab1Button" tab="tab1" href="/tabs/tab1">
          <ion-icon :icon="storefrontOutline" />
          <ion-label>Loja</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon :icon="pricetagsOutline" />
          <ion-label>Meus Cupons</ion-label>
        </ion-tab-button>
        
        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon :icon="cartOutline" />
          <ion-label>Carrinho</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { storefrontOutline, cartOutline, pricetagsOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      storefrontOutline, 
      cartOutline,
      pricetagsOutline
    }
  }
}
</script>

<style scoped>

</style>