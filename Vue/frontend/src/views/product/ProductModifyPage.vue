<template>
    <div>
        <h2>상품 게시물 수정</h2>
        <product-modify-form v-if="product" :poduct="product" @submit="onSubmit"/>
        <p v-else>로딩중입니다 .......</p>
    </div>
</template>

<script>
import ProductModifyForm from '@/components/product/ProductModifyForm.vue';
import { mapActions, mapState } from "vuex";

const ProductModule = "productModule";

export default {
    components: {
        ProductModifyForm,
    },
    props: {
        productId: {
            type: String,
            required: true,
        },
    },
    computed: {
        ...mapState(ProductModule, ["product"]),
    },
    methods: {
        ...mapActions(ProductModule, [
            "requestProductToString", "requestProductModifyToSpring",
        ]),
        async onSubmit(payload){
            const { productName, productPrice, vendor, category } = payload;
            const productId = this.productId;

            await this.requestProductModifyToSpring({
                productName, productPrice, vendor, category
            });

            await this.$router.push({
                name: "ProductReadPage",
                params: { productId: this.productId },
            });
        },
    },
    created() {
        this.requestProductToSpring(this.productId);
    },
};
</script>

<style></style>