<template>
    <form @submit.prevent="handleSubmit">
        <p>Create Product</p>
        <div class="input-container">
            <div class="title-block">
                <label for="title">Title:</label>
                <input v-model="title" type="text" id="title">
            </div>
            <div class="price-block">
                <label for="price">Price:</label>
                <input v-model="price" type="number" id="price">
            </div>
        </div>
        <button type="submit">Add Product</button>
    </form>
</template>

<script>
import { defineComponent, ref } from 'vue';

export default defineComponent({
    emits: ['product-aded'],
    setup(_, { emit }) {
        const title = ref('');
        const price = ref('');
        const handleSubmit = () => {
            emit('product-aded', { title: title.value, price: Number(price.value), id: '@' })
            title.value = '';
            price.value = '';
        }
        return {
            title,
            price,
            handleSubmit
        }
    }
})
</script>

<style scoped>
form {
    padding: 20px;
    border: 1px solid #000;
    border-radius: 15px;
}

.input-container {
    display: grid;
    gap: 10px;
    padding-bottom: 20px;
}

.title-block,
.price-block {
    display: grid;
    grid-template-columns: repeat(2, auto);
    justify-content: end;
    gap: 30px;
}</style>