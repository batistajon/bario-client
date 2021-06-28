<template>
  <ion-page>
    <ion-header collapse="condense">
      <ion-toolbar>
        <ion-title>Perfil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-card>
        <ion-item>
          <ion-avatar slot="start">
            <img src="https://ionicframework.com/docs/demos/api/avatar/avatar.svg"/>
          </ion-avatar>
          <div>
            <h3>Jonathas Batista</h3>
          </div>
        </ion-item>
        <div id="status">
          <ion-card-subtitle>Assinante</ion-card-subtitle>
        </div>
      </ion-card>
      <ion-card>
        <ion-item>
          <ion-label class="itemProfile">Meus Dados</ion-label>
          <ion-icon :icon="personCircleOutline" />
        </ion-item>
        <ion-item>
          <ion-label class="itemProfile">Últimos Pedidos</ion-label>
          <ion-icon :icon="cartOutline" />
        </ion-item>
        <ion-item>
          <ion-label class="itemProfile">Meus pontos</ion-label>
          <ion-icon :icon="trophyOutline" />
        </ion-item>
        <ion-item>
          <ion-label class="itemProfile">Meus Cupons</ion-label>
          <ion-icon :icon="ticketOutline" />
        </ion-item>
        <ion-item>
          <ion-label class="itemProfile">Métodos de Pagamento</ion-label>
          <ion-icon :icon="cardOutline" />
        </ion-item>
        <ion-item>
          <ion-label class="itemProfile">Configurações</ion-label>
          <ion-icon :icon="settingsOutline" />
        </ion-item>
      </ion-card>
    </ion-content>
  </ion-page>
</template>

<script>
import { 
  IonPage, 
  IonHeader, 
  IonToolbar, 
  IonTitle, 
  IonContent,
  IonIcon 
} from '@ionic/vue';
import { 
  chevronForwardOutline,
  personCircleOutline,
  cartOutline,
  trophyOutline,
  ticketOutline,
  cardOutline,
  settingsOutline
} from 'ionicons/icons';

export default  {
  name: 'Tab3',
  components: { 
    IonHeader, 
    IonToolbar, 
    IonTitle, 
    IonContent, 
    IonPage,
    IonIcon 
  },
  setup() {
    return {
      chevronForwardOutline,
      personCircleOutline,
      cartOutline,
      trophyOutline,
      ticketOutline,
      cardOutline,
      settingsOutline
    }
  }
}
</script>
<style>
#status {
  margin-top: 15px;
  margin-left: 80px;
  margin-bottom: 30px;
}
.itemProfile {
  margin: 15px;
}
</style>