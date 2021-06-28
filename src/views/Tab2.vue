<template>
  <ion-page>
    <ion-header collapse="condense">
      <ion-toolbar>
        <ion-title>Meus Cupons</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <cupons-card/>
    </ion-content>
  </ion-page>
</template>

<script>
import { 
  IonPage, 
  IonHeader, 
  IonToolbar, 
  IonTitle, 
  IonContent 
} from '@ionic/vue';
import CuponsCard from '@/components/CuponsCard.vue';

export default  {
  name: 'Tab2',
  components: { 
    IonHeader, 
    IonToolbar, 
    IonTitle, 
    IonContent, 
    IonPage,
    CuponsCard
  }
}
</script>