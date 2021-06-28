<template>
    <ion-chip id="chipCategory" outline="true">
        <ion-label :categoryid="id">{{ label }}</ion-label>
    </ion-chip>
</template>

<script>
import { 
    IonChip, 
    IonLabel 
    } from '@ionic/vue';

export default {
    name: 'Categories',
    props: {
        label: String,
        id:String
    },
    components: {
        IonChip, 
        IonLabel
    }
}
</script>

<style>
#chipCategory {
    display: inline-block;
}
</style>