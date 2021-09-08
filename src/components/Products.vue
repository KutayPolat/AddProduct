<template>
  <div v-if="productList.length > 0">
    <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
    <hr>
    <div class="row product-container">
      <app-product v-for="(product,index) in productList" :key="index">
        <img class="card-img-top" :src="product.selectedImage" :alt="product.title">
        <div class="card-body">
          <h5 class="card-title"> {{ product.title }} </h5>
          <small><strong>Quantity : </strong> {{ product.count }}</small>
          <br>
          <small><strong>Price : </strong> {{ product.price }}</small>
          <br>
          <small><strong>Total Price : </strong> {{ product.totalPrice }}</small>
        </div>
      </app-product>
    </div>
  </div>
</template>

<script>
import Product from "@/components/Product";
import {eventBus} from "@/main";

export default {
  components: {
    appProduct: Product
  },
  data() {
    return {
      productList: [],
    }
  },
  created() {
    eventBus.$emit("productSize",)
    eventBus.$on("productAdded",(product) => {
      if(this.productList.length < 10){
        this.productList.push(product);
        eventBus.$emit("progressBarUpdated",this.productList.length);
      }else {
        alert("You can not add more than 10 product")
      }

    })
  }
}
</script>

<style scoped>

</style>