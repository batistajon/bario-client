<template>
  <ion-page>
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner color="primary"></ion-spinner>
      </div>
    </ion-content>
    <ion-content :fullscreen="true" v-else>
    <ion-header>
      <img id="bannerStore" src="https://bariocafes.com.br/wp-content/uploads/2020/10/201029-bario-site-banner-desktop-02-2.jpg" alt="">
    </ion-header>
      <ion-header collapse="condense">
        <ion-toolbar id="titleImage">
          <a href=""><img width="150" src="https://bariocafes.com.br/wp-content/uploads/2020/06/200615-logo-positivo-300px.png" alt=""></a>
        </ion-toolbar>
      </ion-header>
      <ion-list>
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
  IonToolbar,
  IonTitle, 
  IonContent,
  IonSpinner,
  } from '@ionic/vue';
import { reactive } from 'vue';
import axios from 'axios';
import ProductStoreCard from '@/components/ProductStoreCard.vue'

export default  {
  name: 'Loja',
  components: { 
    IonHeader, 
    IonToolbar, 
    /* IonTitle */
    IonContent, 
    IonPage,
    IonSpinner,
    ProductStoreCard
  },
  setup() {
    const state = reactive({
      products: {},
      loading: false
    });

    const fetchOrders = async (dispLoaderPage: boolean) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res = await axios.get("http://127.0.0.1:8000/api/products");
      
      if(res.data) {
        state.products = res.data;
        console.log(state.products);
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

    return {
      state, 
      fetchOrders, 
      doRefresh
    }
  }
}

</script>
<style scoped>
  #titleImage{
    text-align: center;
  };
  .loading-center {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 90vh;
  };

  ion-spinner {
    transform: scale(1.5);
  };
</style>