<template>
  <ion-page> 
    <ion-content v-if="state.loading">
      <div id="loading-center">
        <ion-spinner color="lines"></ion-spinner>
      </div>
    </ion-content>
    <ion-content color="secondary" :fullscreen="true" v-else>
    <ion-header>
      <img id="bannerStore" src="https://bariocafes.com.br/wp-content/uploads/2020/10/201029-bario-site-banner-desktop-02-2.jpg" alt="">
    </ion-header>
      <ion-header collapse="condense">
        <div id="titleImage" style="padding: 10px;">
          <a href="/tabs/tab1"><img  width="150" src="https://bariocafes.com.br/wp-content/uploads/2020/06/200615-logo-positivo-300px.png" alt=""></a>
        </div>
        <ion-segment 
          color="primary"
          scrollable="true" 
          @ionChange="changeCategory($event)" 
          v-model="state.categories" 
          :value="state.categories"
        >
          <ion-segment-button value="16">
            <ion-label>Cafés</ion-label>
          </ion-segment-button>
          <ion-segment-button value="199">
            <ion-label>Cápsulas</ion-label>
          </ion-segment-button>
          <ion-segment-button value="42">
            <ion-label>Assinatura</ion-label>
          </ion-segment-button>
          <ion-segment-button value="228">
            <ion-label>Kits</ion-label>
          </ion-segment-button>
          <ion-segment-button value="24">
            <ion-label>Cafeteiras</ion-label>
          </ion-segment-button>
          <ion-segment-button value="222">
            <ion-label>Acessorios</ion-label>
          </ion-segment-button>
        </ion-segment>
        </ion-header>
        <ion-list>
        <ion-searchbar placeholder="Procurar produto"></ion-searchbar>
        <div v-for="product in state.products" :key="product.id">
          <product-store-card :product="product" />
        </div>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { IonPage, 
  IonHeader, 
  IonContent,
  IonSpinner,
  IonSegment,
  IonSegmentButton
  } from '@ionic/vue';
import { reactive} from 'vue';
import axios from 'axios';
import ProductStoreCard from '@/components/ProductStoreCard.vue'

export default  {
  name: 'Loja',
  components: { 
    IonHeader, 
    IonContent, 
    IonPage,
    IonSpinner,
    ProductStoreCard,
    IonSegment,
    IonSegmentButton
  },
  setup() {
    const state = reactive({
      products: {},
      loading: false,
      categories: 16
    });

    const fetchOrders = async (dispLoaderPage: boolean) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res = await axios.get(`http://127.0.0.1:8000/api/products/category/${state.categories}`);
      
      if(res.data) {
        state.products = res.data;
      }

      state.loading = false;
    }

    const doRefresh = (event: CustomEvent): void => {
      fetchOrders(false);

      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      event.target?.complete();      
    }

    fetchOrders(true);

    const changeCategory = (e: any) => {
      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      state.categories = e.detail?.value;

      console.log(state.categories);
      fetchOrders(true);
    }

    return {
      state, 
      fetchOrders, 
      doRefresh,
      changeCategory
    }
  }
}

</script>
<style>
  #titleImage{
    text-align: center;
  }
  #loading-center {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 90vh;
  }
  ion-spinner {
    transform: scale(1.5);
  }
  ion-segment-button {
    text-align: center;
    font-weight: bold;
  }
  ion-segment {
    margin: 5px;
  }
</style>