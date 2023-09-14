<template>
<div>
<div class="content" v-if="!productStore.loading">
<div class="panel">
<ProductForm @product-aded="addProduct"/>
<button @click="sortProduct">Sort by price</button>
</div>

<ul class="product-list">
<li v-for="product in productStore.products" :key="product.id">
{{ product.title }} - {{ product.price }}
<div class="number">{{ product.id }}</div>
<button @click="removeProduct(product.id)">Remove</button>
</li>
</ul>
</div>
<Loader v-else/>
</div>
</template>

<script>
import { defineComponent, onMounted } from 'vue';
import Loader from './Loader.vue';
import { useProductStore } from '../store/index';
import ProductForm from './ProductForm.vue';

export default defineComponent({
    setup() {
        const productStore = useProductStore();

        onMounted(() => {
            fetchProduct()
        });
        const fetchProduct = () => {
            productStore.fetchProduct()
        }
         const addProduct = (product) => {
            productStore.addProduct(product)
         }
         const removeProduct = (productId) => {
            productStore.removeProduct(productId)
         }
         const sortProduct = () => {
            productStore.sortProduct()
        }
        return {
            productStore,
            addProduct,
            removeProduct,
            sortProduct
        };
    },
    components: { Loader, ProductForm }
})
</script>

<style scoped>
.panel{
    display: grid;
    grid-template-columns: repeat(2,auto);
    gap: 40px;
    align-items: center;
    justify-items: center;
    justify-content: center;
}
.product-list{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 30px;
}
.product-list li{
    position: relative;

    display: grid;
    align-items: center;
    justify-items: center;
    justify-content: center;
    text-align: center;

    height: 100px;
    padding: 20px;
    border: 1px solid #000;
    border-radius: 15px;
    background: #c6dcc3;
}
.number{
    position: absolute;
    top: 0;
    left: 0;
    padding: 15px;
}
</style>