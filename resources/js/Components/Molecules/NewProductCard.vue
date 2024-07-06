<script setup>
import {ref} from "vue";
import {useStore} from "vuex";

const store = useStore();
const showAnimation = ref(false);
const showSuccess = ref(false);
const addProductToCart = async (product) => {
    showAnimation.value = true;
    try {
        await store.dispatch("cart/add", product);
    } catch (error) {
        showAnimation.value = false;
    } finally {
        showSuccess.value = true;
        setTimeout(function () {
            showSuccess.value = false;
            showAnimation.value = false;
        }, 400);
    }
};
defineProps({
    data: Object,
});
</script>

<template>
    <div class="aspect-h-1 aspect-w-1 w-full overflow-hidden rounded-lg bg-gray-200 xl:aspect-h-8 xl:aspect-w-7">
        <img :src="`https://picsum.photos/1280/1280/?random&id=${data.id}`"
             alt="Tall slender porcelain bottle with natural clay textured body and cork stopper."
             class="h-full w-full object-cover object-center group-hover:opacity-75">
    </div>
    <div class="flex justify-between items-center mt-4">
        <div>
            <h3 class="text-sm text-gray-700">{{ data.name }}</h3>
            <p class="mt-1 text-lg font-medium text-gray-900">$ {{ data.price }}</p>
        </div>
        <button
            @click="addProductToCart(data)"
            class="flex items-center justify-center px-2 py-2 font-medium tracking-wide text-indigo-600 capitalize transition-all duration-500 bg-indigo-50 rounded-xl hover:bg-indigo-100"
        >
                <span class="mx-1">
                    <transition name="fade" class="flex" mode="out-in">
                        <template v-if="!showAnimation">
                            <span class="flex"
                            >

                                <svg
                                    class="h-6 w-6"
                                    fill="none"
                                    viewBox="0 0 24 24"
                                    stroke-width="1.5"
                                    stroke="currentColor"
                                    aria-hidden="true"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        d="M15.75 10.5V6a3.75 3.75 0 10-7.5 0v4.5m11.356-1.993l1.263 12c.07.665-.45 1.243-1.119 1.243H4.25a1.125 1.125 0 01-1.12-1.243l1.264-12A1.125 1.125 0 015.513 7.5h12.974c.576 0 1.059.435 1.119 1.007zM8.625 10.5a.375.375 0 11-.75 0 .375.375 0 01.75 0zm7.5 0a.375.375 0 11-.75 0 .375.375 0 01.75 0z"
                                    ></path>
                                </svg>
<!--                                <span>Add to cart</span>-->
                            </span>
                        </template>
                        <template v-else>
                            <div>
                                <div role="status" v-if="!showSuccess">
                                    <svg
                                        aria-hidden="true"
                                        class="w-4 h-4 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
                                        viewBox="0 0 100 101"
                                        fill="none"
                                        xmlns="http://www.w3.org/2000/svg"
                                    >
                                        <path
                                            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                                            fill="currentColor"
                                        />
                                        <path
                                            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                                            fill="currentFill"
                                        />
                                    </svg>
                                    <span class="sr-only">Loading...</span>
                                </div>
                                <span v-else
                                      class="flex">
                                    <svg

                                        version="1.1"
                                        id="Capa_1"
                                        class="w-5 h-5 text-gray-200 animate-bounce animate-ping dark:text-white fill-green"
                                        viewBox="0 0 50 50"
                                        xmlns="http://www.w3.org/2000/svg"
                                        xmlns:xlink="http://www.w3.org/1999/xlink"
                                        xml:space="preserve"
                                    >
                                    <g
                                        id="SVGRepo_bgCarrier"
                                        stroke-width="0"
                                    ></g>
                                    <g
                                        id="SVGRepo_tracerCarrier"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                    ></g>
                                    <g id="SVGRepo_iconCarrier">
                                        <circle
                                            style="fill: #25ae88"
                                            cx="25"
                                            cy="25"
                                            r="25"
                                        ></circle>
                                        <polyline
                                            style="
                                                fill: none;
                                                stroke: #ffffff;
                                                stroke-width: 2;
                                                stroke-linecap: round;
                                                stroke-linejoin: round;
                                                stroke-miterlimit: 10;
                                            "
                                            points=" 38,15 22,33 12,25 "
                                        ></polyline>
                                    </g>
                                </svg>
<!--                                <span class="mx-1 text-[#25ae88]">Add Success</span>-->
                                </span>
                            </div>
                        </template>
                    </transition>
                </span>
        </button>
    </div>
</template>
<style scoped>
.fade-leave-active {
    transition: opacity 0.2s;
}

.fade-enter,
.fade-leave-to {
    opacity: 0;
}
</style>
