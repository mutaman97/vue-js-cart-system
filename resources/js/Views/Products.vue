<script setup>
import {toRaw} from "vue";
import {useStore} from "vuex";
import {Head} from "@inertiajs/vue3";
import ProductsList from "@/Components/Organisms/ProductsList.vue";
import BlankLayout from "@/Layouts/BlankLayout.vue";
import NewProductsList from "@/Components/Organisms/NewProductsList.vue";

const props = defineProps({
    products: Object,
    cartItems: Object,
});

const store = useStore();
const existingCartItems = toRaw(props.cartItems).data;
const products = toRaw(props.products).data;
store.dispatch("cart/set", existingCartItems);
</script>

<template>
    <blank-layout>
        <section class="py-24">
            <div class="bg-white">
                <div class="mx-auto max-w-2xl px-4 py-16 sm:px-6 sm:py-24 lg:max-w-7xl lg:px-8">
                    <h2 class="font-manrope font-bold text-4xl text-black mb-8 max-lg:text-center">Products</h2>
                    <NewProductsList :items="products"/>
                </div>
            </div>
        </section>
    </blank-layout>
</template>
