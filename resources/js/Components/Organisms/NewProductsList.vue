<script setup>
import {computed} from "vue";
import ProductCard from "@/Components/Molecules/ProductCard.vue";
import NewProductCard from "@/Components/Molecules/NewProductCard.vue";

defineProps({
    items: Array,
});
</script>

<template>
    <div class="grid grid-cols-2 gap-x-3 gap-y-10 sm:grid-cols-3 sm:gap-x-4 md:grid-cols-3 md:gap-x-6 lg:grid-cols-3 lg:gap-x-6 xl:grid-cols-4 xl:gap-x-8">
        <div v-for="(item, index) in items"
             class="group">
            <new-product-card :key="index" :data="item"/>
        </div>
    </div>
</template>
