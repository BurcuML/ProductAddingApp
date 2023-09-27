<template>
    <div v-if="ProductList.length > 0">
        <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
    <hr>
     <div class="row product-container">
        <appProduct v-for="product in ProductList">
            <img class="card-img-top" :src="product.selectedImage" alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title">{{product.title}}</h5>
          <small>
            <strong>Adet : </strong> {{product.count}}
          </small>
          <br>
          <small>
            <strong>Fiyat : </strong> {{product.price}}
          </small>
          <br>
          <small>
            <strong>Tutar : </strong> {{product.totalPrice}}
          </small>
        </div>
        </appProduct>
     </div>
    </div>
</template>
<script>
import Product from './Product.vue';
import { eventBus } from '../main';

export default{
    components:{
        appProduct: Product
    },
    data(){
        return{
            ProductList: [],

        }
    },

    created(){
        eventBus.$on("productAdded", (product) => {
            this.ProductList.push(product);
            if(this.ProductList.length <=5){
                eventBus.$emit("progressBar", this.ProductList.length);
            }else{
                alert("Daha fazla ürün ekleyemezsiniz!");
            }
        });
    }
}
</script>