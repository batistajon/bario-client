<template>
  <ion-page>
      <ion-header>
          <ion-toolbar>
              <ion-buttons slot="start">
                  <ion-back-button></ion-back-button>
              </ion-buttons>
              <ion-title>{{ state.product.name }}</ion-title>
          </ion-toolbar>
      </ion-header>
      <ion-content v-if="state.loading">
          <div id="loading-center">
            <ion-spinner color="primary"></ion-spinner>
        </div>
      </ion-content>
      <ion-content :fullscreen="true" v-else>
          <ion-card>
            <div id="divImgAddCart"> 
                <img id="imgAddCart" :src="state.product.images[0].src" alt="">  
            </div>  
            <ion-card-header>
                <ion-card-subtitle>{{ state.product.name }}</ion-card-subtitle>
                <ion-card-title>R$ {{ state.product.price }}</ion-card-title>
            </ion-card-header>
            <ion-card-content id="description">
                <p>{{inner(state.product.description)}}</p>
            </ion-card-content> 
            <ion-item v-for="attr in state.product.attributes" :key="attr.id">
                <ion-label>{{attr.name}}</ion-label>
                <ion-select>
                        <ion-select-option 
                            v-for="option in attr.options" 
                            :key="option" 
                            :value="option">{{ option }}
                        </ion-select-option>
                </ion-select>
            </ion-item>
            <ion-item>
                <ion-label>Quantidade</ion-label>
                <ion-select value="1" v-model="state.qtt">
                    <ion-select-option value="1">1</ion-select-option>
                    <ion-select-option value="2">2</ion-select-option>
                    <ion-select-option value="3">3</ion-select-option>
                    <ion-select-option value="4">4</ion-select-option>
                    <ion-select-option value="5">5</ion-select-option>
                    <ion-select-option value="6">6</ion-select-option>
                    <ion-select-option value="7">7</ion-select-option>
                    <ion-select-option value="8">8</ion-select-option>
                    <ion-select-option value="9">9</ion-select-option>
                    <ion-select-option value="10">10</ion-select-option>
                </ion-select>
            </ion-item>
            <div id="divButtonAddCart">
                <ion-button expand="block">
                    Adicionar ao carrinho
                </ion-button>
            </div>
        </ion-card>
          
      </ion-content>
  </ion-page>
</template>

<script>
import {
    IonBackButton, 
    IonButtons,
    IonToolbar,
    IonHeader,
    IonPage,
    IonSpinner,
    IonContent, 
    IonIcon,
} from '@ionic/vue';
import { addOutline, removeOutline } from 'ionicons/icons'
import { reactive } from "vue";
import { useRouter, useRoute } from 'vue-router';
import axios from 'axios';
    
export default {
    name: "ProductAddCart",
    components: {
        IonBackButton, 
        IonButtons,
        IonToolbar,
        IonHeader,
        IonPage,
        IonSpinner,
        IonContent, 
        //IonIcon
    },
    setup() {
        const router = useRouter();
        const route = useRoute();
        const product = route.params;

        const state = reactive({
            product: {},
            loading: false,
            qtt: 1
        });

        const fetchProductByid = async (id) => {
            state.loading = true;

            const res = await axios.get(`https://api.winassessoria.com/api/products/details/${id}`);

            if(res.data) {
                state.product = res.data
            }

            state.loading = false;
        }

        const inner = (param) => {
            const regex = /(<[^>]+>|<[^>]>|<\/[^>]>)/g;
            return param.replace(regex, '');
        }

        const addOrRemoveCart = (param) => {

            console.log(param);
        }

        fetchProductByid(product.id); 
        
        return {
            router,
            state,
            product,
            inner,
            addOutline,
            removeOutline,
            addOrRemoveCart
        }
    }
}
</script>

<style>
    #loading-center {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 90vh;
  }
  ion-spinner {
    transform: scale(1.5);
  }
  #imgAddCart {
    max-width: 350px;
    max-height: 350px;
  }
  #divImgAddCart {
    text-align: center;
    align-content: center;
  }
  #inputCartQtt {
    text-align: center;
  }
  #divButtonAddCart {
    margin:15px 15px 20px 15px;
  }
</style>