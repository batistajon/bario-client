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
                <div id="buttonCart">
                    <ion-item>
                        <ion-icon :icon="addOutline" @click="addOrRemoveCart($event)" value="add"/>
                        <ion-input 
                            id="inputCartQtt" 
                            type="number" 
                            v-model="state.qtt" 
                            :value="state.qtt"
                        ></ion-input>
                        <ion-icon :icon="removeOutline" @click="addOrRemoveCart($event)" value="remove"/>
                    </ion-item>
                </div>
            </ion-card-content>
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
        IonIcon
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

            const res = await axios.get(`http://127.0.0.1:8000/api/products/${id}`);

            if(res.data) {
                state.product = res.data
            }

            state.loading = false;
        }

        const inner = (param) => {
            const regex = /(<[^>]+>|<[^>]>|<\/[^>]>)/g;
            return param.replace(regex, '');
        }

        const addOrRemoveCart = (e) => {

            state.qtt = e;
            console.log(state.qtt);
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
  #buttonCart {
      width: 120px;
      margin-top: 10px;
  }
  #inputCartQtt {
      text-align: center;
  }
</style>