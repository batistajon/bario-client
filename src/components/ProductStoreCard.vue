<template>
  <ion-card @click="routePush(product.id)">
    <ion-grid fixed>
      <ion-row>
        <ion-col size="4" v-for="image in product.images" :key="image.id">
          <img v-if="image == null" src="/resource/icon.png" alt="">
          <img v-else id="thumbCard" :src="image.src">
        </ion-col>
        <ion-col size="8">
          <ion-item>
            <ion-label>
              <h4><strong>{{product.name}}</strong></h4>
              <p>{{ inner(product.description) }}</p>
            </ion-label>
          </ion-item>
          <div id="priceCard">
            <p>por R$ <strong style="font-size: 20px;">{{ product.price }}</strong></p> 
          </div>
        </ion-col>
      </ion-row>
    </ion-grid>
  </ion-card>
</template>

<script>
import {useRouter, useRoute}  from 'vue-router';

export default {
  name: "ProductStoreCard",
  props: {
    product: Object
  },
  setup() {
    const router = useRouter();
    const route = useRoute();

    const inner = (param) => {
      const regex = /(<[^>]+>|<[^>]>|<\/[^>]>)/g;
      return param.replace(regex, '');
    }

    const routePush = (id) => {router.push(`/product-add-cart/${id}`)}

    return {
      routePush,
      inner,
      route
    }
  }
}
</script>

<style>
  #thumbCard{
    text-align: center;
    max-height: 100px;
    align-items: center;
    align-content: center;
  }
  #priceCard{
    margin-left: 20px;
  }
</style>