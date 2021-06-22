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
        <ion-searchbar placeholder="Procurar produto"></ion-searchbar>
        <product-store-card
          v-for="product in state.products" :key="product.id"
          :product="product"
        />
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { 
  IonPage, 
  IonContent,
  IonSpinner
  } from '@ionic/vue';
import { reactive} from 'vue';
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
      products: {},
      loading: false,
      categoryId: 16,
      categories: {}
    });

    const fetchCategories = async (dispLoaderPage: boolean) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res = await axios.get(`http://127.0.0.1:8000/api/products/categories`);

      if(res.data) {
        state.categories = res.data;
        console.log(res.data);
      }
    }

    const fetchOrders = async (dispLoaderPage: boolean) => {

      if(dispLoaderPage) {
        state.loading = true;
      }

      const res2 = await axios.get(`http://127.0.0.1:8000/api/products/category/${state.categoryId}`);


      if(res2.data) {
        state.products = res2.data;
      }

      state.loading = false;
    }

    const doRefresh = (event: CustomEvent): void => {
      fetchOrders(false);

      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      event.target?.complete();      
    }

    fetchCategories(true);
    fetchOrders(true);

    const changeCategory = (e: any) => {
      // eslint-disable-next-line @typescript-eslint/ban-ts-ignore
      // @ts-ignore
      state.categoryId = e.target.attributes.categoryid.value;

      console.log(e.target.attributes.categoryid.value);
      //fetchCategories(true);
      fetchOrders(true);
    }

    return {
      state, 
      fetchOrders, 
      fetchCategories,
      doRefresh,
      changeCategory
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