<template>
  <ion-page>
    <ion-tabs> 
      <ion-tab-bar color="secondary" slot="bottom"  id="baseBar">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <ion-icon :icon="storefrontOutline" />
          <ion-label>Loja</ion-label>
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon :icon="pricetagOutline" />
          <ion-label>Meus cupons</ion-label>
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon :icon="personOutline" />
          <ion-label>Perfil</ion-label>
        </ion-tab-button>
        
        <ion-tab-button tab="tab4" href="/tabs/tab4">
        <ion-badge color="primary">11</ion-badge>
          <ion-icon :icon="cartOutline" />
          <ion-label>Carrinho</ion-label>
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonLabel, IonIcon, IonPage } from '@ionic/vue';
import { storefrontOutline, cartOutline, pricetagOutline, personOutline, bagHandleOutline } from 'ionicons/icons';

export default {
  name: 'Tabs',
  components: { IonLabel, IonTabs, IonTabBar, IonTabButton, IonIcon, IonPage },
  setup() {
    return {
      storefrontOutline, 
      cartOutline,
      pricetagOutline,
      personOutline,
      bagHandleOutline
    }
  }
}
</script>

<style scoped>

</style>