<template>
  <ion-card>
    <ion-card-header>
      <ion-item>
      <ion-thumbnail slot="start" v-for="image in product.images" :key="image.id">
        <img :src="image.src">
      </ion-thumbnail>
      <ion-label>
        <h3><strong>{{product.name}}</strong></h3>
        <p>Por: <strong>{{ product.price }},00</strong></p>
      </ion-label>
    </ion-item>
    </ion-card-header>
    <ion-card-content>
      Cafe especial
    </ion-card-content>
  </ion-card>
</template>

<script>
export default {
  name: "ProductStoreCard",
  props: {
    product: Object
  }
}
</script>

<style>

</style>