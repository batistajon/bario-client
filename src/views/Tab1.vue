<template>
  <ion-page> 
    <ion-content v-if="state.loading">
      <div class="loading-center">
        <ion-spinner color="lines"></ion-spinner>
      </div>
    </ion-content>
    <ion-content :fullscreen="true" v-else>
      <img
       id="bannerStore" 
       src="https://bariocafes.com.br/wp-content/uploads/2021/06/site-5.png"
      >
      <ion-list>
        <div id="categories">
            <swiper-categories 
              v-for="category in state.categories" :key="category.id"
              :label="category.name"
              :id="category.id"
              @click="changeCategory($event)"
            />
        </div> 
        <ion-searchbar
          @keyup="resultadoBusca($event.target.value)"
          placeholder="Digite 3 caracteres " 
          v-model="state.busca"
        ></ion-searchbar>
        <div v-if="state.loadingBusca">
          <div class="loading-center">
            <ion-spinner color="lines"></ion-spinner>
          </div>
        </div>
        <div v-else>
          <product-store-card
            v-for="product in state.products" :key="product.id"
            :product="product"
          />
        </div>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script>
import { 
  IonPage, 
  IonContent,
  IonSpinner
  } from '@ionic/vue';
import { reactive } from 'vue';
import axios from 'axios';
import ProductStoreCard from '@/components/ProductStoreCard.vue';
import SwiperCategories from '@/components/SwiperCatergories.vue';

export default  {
  name: 'Loja',
  components: { 
    IonContent, 
    IonPage,
    IonSpinner,
    ProductStoreCard,
    SwiperCategories
  },
  setup() {
    const state = reactive({
      products: Array,
      loading: false,
      categoryId: 16,
      categories: Array,
      buscaId: [],
      busca: String,
      loadingBusca: false
    });

    const fetchCategories = async (dispLoaderPage) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res = await axios.get(`https://api.winassessoria.com/api/products/categories`);

      if(res.data) {
        state.categories = res.data;
      }
    }

    const fetchOrders = async (dispLoaderPage) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res2 = await axios.get(`https://api.winassessoria.com/api/products/category/${state.categoryId}`);

      if(res2.data) {
        state.products = res2.data;
      }

      state.loading = false;
      //console.log(state.busca)
    }

    const doRefresh = (event) => {
      fetchOrders(false);

      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      event.target?.complete();      
    }

    fetchCategories(true);
    fetchOrders(true);

    const changeCategory = (e) => {
      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      state.categoryId = e.target.attributes.categoryid.value;

      fetchOrders(true);
    }

    const resultadoBusca = async (e) => {

      if(e.length >= 3) {

        state.loadingBusca = true;

        const res3 = await axios.get(`https://api.winassessoria.com/api/products`);

        if(res3.data) {
          state.products = res3.data;
        }

        let element = Object;
        let result = Boolean;

        for (let i = 0; i < state.products.length; i++) {
          
          element = state.products[i];
          result = element.slug.indexOf(e, -1) > -1;

          if(result) {
            state.buscaId.push(element.id)
          }
        }

        console.log(state.buscaId);

        const res5 = axios.post(`https://api.winassessoria.com/api/products`, JSON.parse(state.buscaId))
         
        if(res5.data) {
          state.products = res5.data;
        }

        state.buscaId = [];
        state.loadingBusca = false;
        console.log(state.buscaId, 'vazio');
      }
    }

    return {
      state, 
      fetchOrders, 
      fetchCategories,
      doRefresh,
      changeCategory,
      resultadoBusca
    }
  }
}

</script>
<style>
  #titleImage{
    margin-top: 15px;
    text-align: center;
  }
  .loading-center {
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
    margin-left: 5px;
    margin-right: 5px;
    width: 200px;
  }
  .labelSegBtn {
    margin-left: 5px;
    margin-right: 5px;
  }
  ion-segment {
    margin: 5px;
  }
  #categories {
    margin: 10px 10px 0px 10px;
    overflow: auto;
    white-space: nowrap;
  }
</style>