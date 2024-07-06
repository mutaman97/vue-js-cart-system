<script setup>
import {computed} from "vue";
import ProductCard from "@/Components/Molecules/ProductCard.vue";
import NewProductCard from "@/Components/Molecules/NewProductCard.vue";

defineProps({
    items: Array,
});
</script>

<template>
    <div class="grid grid-cols-1 gap-x-6 gap-y-10 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 xl:gap-x-8">
        <div v-for="(item, index) in items"
             class="group">
            <new-product-card :key="index" :data="item"/>
        </div>
    </div>
</template>
