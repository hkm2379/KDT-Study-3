<template>
    <div>
        <h2>Product Page</h2>
        <product-read-form v-if="product" :product="product"/>
        <p v-else>Loading ...</p>
        <router-link :to="{ name: 'ProductModifyPage', params: { productId }}">
            Modify Page
        </router-link>
        <button @click="onDelete">
            Delete
        </button>
        <router-link :to="{ name:'ProductListPage' }">
            To PageList
        </router-link>
    </div>
</template>

<script>
import ProductReadForm from '@/components/product/ProductReadForm.vue';
import { mapActions, mapState } from 'vuex';

const productModule = 'productModule'

export default {
    components: {
        ProductReadForm
    },
    props: {
        productId: {
            type: String,
            required: true,
        }
    },
    computed: {
        ...mapState(productModule,['product'])
    },

    methods: {     
        ...mapActions(
            productModule, ['requestProductToSpring']
        ),
    },
    created() {
            this.requestProductToSpring(this.productId)
    },
    async onDelete () {
            await this.requestDeleteProductToSpring(this.productId)
            await this.$router.push({ name: 'ProductListPage' })
        }
    }
</script>

<style></style>