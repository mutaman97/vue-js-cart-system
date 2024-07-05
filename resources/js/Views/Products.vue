<script setup>
import { toRaw } from "vue";
import { useStore } from "vuex";
import { Head } from "@inertiajs/vue3";
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
<!--    <Head title="Home" />-->
<!--    <DefaultLayout>-->
<!--        <template #header>-->
<!--            <h2 class="font-semibold text-xl text-gray-800 leading-tight">-->
<!--                Products-->
<!--            </h2>-->
<!--        </template>-->
<!--        <section class="mt-14 flex-1">-->
<!--            <ProductsList :items="products" />-->
<!--        </section>-->
<!--    </DefaultLayout>-->

    <blank-layout>
        <section class="py-24">
            <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
                <h2 class="font-manrope font-bold text-4xl text-black mb-8 max-lg:text-center">
                    Product list
                </h2>
                <NewProductsList :items="products" />
            </div>
        </section>
    </blank-layout>
</template>
