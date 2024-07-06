<script setup>
import { toRaw, computed } from "vue";
import { useStore } from "vuex";
import {
    Dialog,
    DialogPanel,
    DialogTitle,
    TransitionChild,
    TransitionRoot,
} from "@headlessui/vue";

import { XMarkIcon } from "@heroicons/vue/24/outline";

const store = useStore();

const cartItems = computed(() => store.getters["cart/items"]);
const hasItemsInCart = computed(() => cartItems.value.length > 0);
const isCartOpen = computed(() => store.getters["cart/isOpen"]);
const totalPrice = computed(() => store.getters["cart/totalPrice"]);
const removeFromCart = (index) => {
    store.dispatch("cart/remove", index);
};

const toggleCart = () => {
    store.dispatch("cart/toggle");
};

const incrementQuantity = (index) => {
    store.dispatch("cart/increment", index);
};

const decrementQuantity = (index) => {
    store.dispatch("cart/decrement", index);
};
const updateQuantity = (index, quantity) => {
    store.commit("cart/update", { index, quantity });
};
</script>

<template>
    <TransitionRoot as="template" :show="isCartOpen">
        <Dialog as="div" class="relative z-10" @close="toggleCart()">
            <TransitionChild
                as="template"
                enter="ease-in-out duration-500"
                enter-from="opacity-0"
                enter-to="opacity-100"
                leave="ease-in-out duration-500"
                leave-from="opacity-100"
                leave-to="opacity-0"
            >
                <div
                    class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"
                />
            </TransitionChild>

            <div class="fixed inset-0 overflow-hidden">
                <div class="absolute inset-0 overflow-hidden">
                    <div
                        class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10"
                    >
                        <TransitionChild
                            as="template"
                            enter="transform transition ease-in-out duration-500 sm:duration-700"
                            enter-from="translate-x-full"
                            enter-to="translate-x-0"
                            leave="transform transition ease-in-out duration-500 sm:duration-700"
                            leave-from="translate-x-0"
                            leave-to="translate-x-full"
                        >
                            <DialogPanel
                                class="pointer-events-auto w-screen max-w-md"
                            >
                                <div
                                    class="flex h-full flex-col overflow-y-scroll bg-white shadow-xl"
                                >
                                    <div
                                        class="flex-1 overflow-y-auto px-4 py-6 sm:px-6"
                                    >
                                        <div
                                            class="flex items-start justify-between"
                                        >
                                            <DialogTitle
                                                class="text-lg font-medium text-gray-900"
                                                >Shopping cart</DialogTitle
                                            >
                                            <div
                                                class="ml-3 flex h-7 items-center"
                                            >
                                                <button
                                                    type="button"
                                                    class="-m-2 p-2 text-gray-400 hover:text-gray-500"
                                                    @click="toggleCart()"
                                                >
                                                    <span class="sr-only"
                                                        >Close panel</span
                                                    >
                                                    <XMarkIcon
                                                        class="h-6 w-6"
                                                        aria-hidden="true"
                                                    />
                                                </button>
                                            </div>
                                        </div>




                                        <div v-if="hasItemsInCart"
                                            class="mt-8">
                                            <div class="flow-root">
                                                <ul
                                                    role="list"
                                                    class="-my-6 divide-y divide-gray-200"
                                                >
                                                    <li
                                                        v-for="(
                                                            product, index
                                                        ) in cartItems"
                                                        :key="index"
                                                        class="flex py-6"
                                                    >
                                                        <div
                                                            class="h-24 w-24 flex-shrink-0 overflow-hidden rounded-md border border-gray-200"
                                                        >
                                                            <img
                                                                :src="`https://picsum.photos/600/400/?random${index}`"
                                                                class="h-full w-full object-cover object-center"
                                                            />
                                                        </div>

                                                        <div
                                                            class="ml-4 flex flex-1 flex-col"
                                                        >
                                                            <div>
                                                                <div
                                                                    class="flex justify-between text-base font-medium text-gray-900"
                                                                >
                                                                    <h3>
                                                                        <a
                                                                            href="#"
                                                                            >{{
                                                                                product.name
                                                                            }}</a
                                                                        >
                                                                    </h3>
                                                                    <p
                                                                        class="ml-4"
                                                                    >
                                                                        {{
                                                                            product.price
                                                                        }}
                                                                    </p>
                                                                </div>
                                                                <p
                                                                    class="mt-1 text-sm text-gray-500"
                                                                >
                                                                    {{
                                                                        product.color
                                                                    }}
                                                                </p>
                                                            </div>
                                                            <div
                                                                class="flex flex-1 items-end justify-between text-sm"
                                                            >
                                                                <div
                                                                    class="custom-number-input pr-5"
                                                                >
                                                                    <div
                                                                        class="flex flex-row gap-2 h-10 w-full rounded-lg relative bg-transparent mt-1"
                                                                    >


                                                                        <button @click="decrementQuantity(index)"
                                                                            class="group rounded-[50px] border border-gray-200 shadow-sm shadow-transparent p-2.5 flex items-center justify-center bg-white transition-all duration-500 hover:shadow-gray-200 hover:bg-gray-50 hover:border-gray-300 focus-within:outline-gray-300">
                                                                            <svg class="stroke-gray-900 transition-all duration-500 group-hover:stroke-black"
                                                                                 width="18" height="19" viewBox="0 0 18 19" fill="none"
                                                                                 xmlns="http://www.w3.org/2000/svg">
                                                                                <path d="M4.5 9.5H13.5" stroke="" stroke-width="1.6" stroke-linecap="round"
                                                                                      stroke-linejoin="round" />
                                                                            </svg>
                                                                        </button>
                                                                        <input type="number" id="number"
                                                                               class="border border-gray-200 rounded-full w-10 aspect-square outline-none text-gray-900 font-semibold text-sm py-1.5 px-3 bg-gray-100  text-center"
                                                                               placeholder="2"
                                                                               v-model.number="product.selectedQuantity"
                                                                               min="1"
                                                                               @input="
                                                                                updateQuantity(index, product.selectedQuantity)"
                                                                        >
                                                                        <button
                                                                            @click="incrementQuantity(index)"
                                                                            class="group rounded-[50px] border border-gray-200 shadow-sm shadow-transparent p-2.5 flex items-center justify-center bg-white transition-all duration-500 hover:shadow-gray-200 hover:bg-gray-50 hover:border-gray-300 focus-within:outline-gray-300">
                                                                            <svg class="stroke-gray-900 transition-all duration-500 group-hover:stroke-black"
                                                                                 width="18" height="19" viewBox="0 0 18 19" fill="none"
                                                                                 xmlns="http://www.w3.org/2000/svg">
                                                                                <path d="M3.75 9.5H14.25M9 14.75V4.25" stroke="" stroke-width="1.6"
                                                                                      stroke-linecap="round" stroke-linejoin="round" />
                                                                            </svg>
                                                                        </button>
                                                                    </div>
                                                                </div>
                                                                <div
                                                                    class="flex"
                                                                >
                                                                    <button
                                                                        @click="
                                                                            removeFromCart(
                                                                                index
                                                                            )
                                                                        "
                                                                        type="button"
                                                                        class="font-medium text-indigo-600 hover:text-indigo-500"
                                                                    >
                                                                        Remove
                                                                    </button>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </li>
                                                </ul>
                                            </div>
                                        </div>
                                        <div
                                            v-else
                                        class="mt-20 text-center">
                                            Oops! your cart is empty.
                                        </div>
                                    </div>

                                    <div
                                        class="border-t border-gray-200 px-4 py-6 sm:px-6"
                                    >
                                        <div
                                            class="flex justify-between text-base font-medium text-gray-900"
                                        >
                                            <p>Subtotal</p>
                                            <p>${{ totalPrice.toFixed(2) }}</p>
                                        </div>
                                        <p class="mt-0.5 text-sm text-gray-500">
                                            Shipping and taxes calculated at
                                            checkout.
                                        </p>
                                        <div class="mt-6">
                                            <a
                                                href="#"
                                                class="flex items-center justify-center rounded-md border border-transparent bg-indigo-600 px-6 py-3 text-base font-medium text-white shadow-sm hover:bg-indigo-700"
                                                >Checkout</a
                                            >
                                        </div>
                                        <div
                                            class="mt-6 flex justify-center text-center text-sm text-gray-500"
                                        >
                                            <p>
                                                or
                                                <button
                                                    type="button"
                                                    class="font-medium text-indigo-600 hover:text-indigo-500"
                                                    @click="toggleCart"
                                                >
                                                    Continue Shopping
                                                    <span aria-hidden="true">
                                                        &rarr;</span
                                                    >
                                                </button>
                                            </p>
                                        </div>
                                    </div>
                                </div>
                            </DialogPanel>
                        </TransitionChild>
                    </div>
                </div>
            </div>
        </Dialog>
    </TransitionRoot>
</template>
<style scoped>
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

.custom-number-input input:focus {
    outline: none !important;
}

.custom-number-input button:focus {
    outline: none !important;
}
</style>
