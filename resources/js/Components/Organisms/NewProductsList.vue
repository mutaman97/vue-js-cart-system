<script setup>
import { computed } from "vue";
import ProductCard from "@/Components/Molecules/ProductCard.vue";
import NewProductCard from "@/Components/Molecules/NewProductCard.vue";

defineProps({
    items: Array,
});
</script>
<template>
<!--    <div class="flex flex-wrap -mx-1 lg:-mx-4">-->
<!--        <div-->
<!--            v-for="(item, index) in items"-->
<!--            class="my-1 px-1 w-full md:w-1/2 lg:my-4 lg:px-4 lg:w-1/3"-->
<!--        >-->
<!--            <product-card :key="index" :data="item" />-->
<!--        </div>-->
<!--    </div>-->


<!--    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">-->
<!--        <a  v-for="(item, index) in items"-->
<!--            href="javascript:;" class="mx-auto sm:mr-0 group cursor-pointer lg:mx-auto bg-white transition-all duration-500">-->
<!--            <new-product-card :key="index" :data="item" />-->
<!--        </a>-->
<!--    </div>-->


    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
        <a v-for="(item, index) in items"
            href="javascript:;" class="relative bg-cover group rounded-3xl bg-center overflow-hidden mx-auto sm:ml-0 xl:mx-auto cursor-pointer">
            <new-product-card :key="index" :data="item" />
        </a>
    </div>
</template>
