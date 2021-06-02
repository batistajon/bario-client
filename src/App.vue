<template>
  <ion-app>
    <ion-router-outlet />
  </ion-app>
</template>

<script lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  components: {
    IonApp,
    IonRouterOutlet
  }
});
</script>
<style scoped>
@font-face {
    font-family:'Fashion Fetish Heavy';
    src:url("/resource/Fashion Fetish Heavy.ttf");
}
</style>