<template>
  <div>
      <ion-input type="text" placeholder="Awesome Input" @keyup="findProducts($event.target.value)"></ion-input>  
  </div>
  {{busca}}
</template>

<script>
export default {
    name: 'SearchProducts',
    data() {
        return {
            busca: ''
        }
    }, 
    methods: {
        findProducts(e) {
            this.busca = e
            console.log(e)
        }
    }
}
</script>

<style>

</style>