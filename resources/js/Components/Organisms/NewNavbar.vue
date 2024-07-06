<script setup>
import {ref, computed, toRaw} from "vue";
import {Link} from "@inertiajs/vue3";
import {useStore} from "vuex";
import Dropdown from "@/Components/Atoms/Dropdown.vue";
import DropdownLink from "@/Components/Atoms/DropdownLink.vue";

const store = useStore();
const showMenu = ref(false);
const totalCartItems = computed(() => toRaw(store.getters["cart/total"]));

function toggleNavbar() {
    showMenu.value = !showMenu.value;
}

const toggleCart = () => {
    store.dispatch("cart/toggle");
};
</script>
<template>
    <nav
        class="py-5 border-b-default border-solid border-gray-200 z-10 w-full bg-inherit"
        id="topnav"
    >
        <div class="mx-auto max-w-7xl  lg:px-8">
            <div class="w-full flex flex-col lg:flex-row">
                <div class="flex justify-between lg:hidden px-4">
                    <Link href="/" class="flex items-center">
                        <svg
                            version="1.1"
                            id="Layer_1"
                            xmlns="http://www.w3.org/2000/svg"
                            xmlns:xlink="http://www.w3.org/1999/xlink"
                            x="0px"
                            y="0px"
                            width="31.06px"
                            height="30.16px"
                            viewBox="0 0 31.06 30.16"
                            style="enable-background:new 0 0 31.06 30.16;"
                            xml:space="preserve"
                        >
                          <g>
                            <path
                                style="fill:#5FECFD;"
                                d="M7.62,14.76l0.54,0.37l-7.4-4.97C0.29,9.84,0.01,9.31,0.01,8.75L0,1.11C0,0.22,0.99-0.3,1.73,0.19l13.8,9.26 L7.62,14.76z"
                            />
                              <path
                                  style="opacity:0.4; fill:#0147DC;"
                                  d="M22.86,15.15l-6.54,4.41c-0.23,0.16-0.51,0.24-0.78,0.24c0.26-0.01,0.52-0.08,0.74-0.23L22.86,15.15z"
                              />
                              <polygon
                                  style="fill:#0046D9;"
                                  points="23.44,14.76 15.53,9.45 16.59,8.74"
                              />
                              <path
                                  style="fill:#0153FF;"
                                  d="M31.06,1.11l-0.01,7.63c0,0.57-0.28,1.1-0.75,1.41l-6.86,4.6l0,0l-6.85-6.02l12.74-8.55 C30.07-0.3,31.06,0.22,31.06,1.11z"
                              />
                              <path
                                  style="fill:#00BDF7;"
                                  d="M23.44,14.76l-0.58,0.39l-6.57,4.41c-0.22,0.15-0.48,0.23-0.74,0.23h-0.02c-0.26-0.01-0.52-0.08-0.74-0.23 l-6.61-4.44l-0.54-0.37l7.91-5.31L23.44,14.76z"
                              />
                              <path
                                  style="opacity:0.4; fill:#0147DC;"
                                  d="M14.78,19.56c0.22,0.15,0.48,0.23,0.74,0.23c-0.27,0-0.54-0.08-0.78-0.24l-6.58-4.43L14.78,19.56z"
                              />
                              <polygon
                                  style="opacity:0.4; fill:#0147DC;"
                                  points="23.44,14.76 22.86,15.15 23.44,14.76"
                              />
                              <path
                                  style="fill:#0153FF;"
                                  d="M7.08,25.84c-2.01,1.4-4.03,2.8-6.04,4.2C0.6,30.34,0,30.03,0,29.49v-8.34c0-0.51,0.57-0.82,1-0.54l6.07,4.02 C7.5,24.92,7.51,25.55,7.08,25.84z"
                              />
                              <path
                                  style="fill:#5FECFD;"
                                  d="M31.06,21.15v8.34c0,0.54-0.6,0.85-1.04,0.54c-2.01-1.4-4.03-2.8-6.04-4.2c-0.42-0.29-0.42-0.92,0.01-1.21 l6.07-4.02C30.49,20.33,31.06,20.64,31.06,21.15z"
                              />
                          </g>
                        </svg>
                    </Link>
                    <button
                        data-collapse-toggle="navbar"
                        type="button"
                        class="inline-flex items-center p-2 ml-3 text-sm text-gray-500 rounded-lg lg:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200"
                        aria-controls="navbar-default"
                        aria-expanded="false"
                        v-on:click="toggleNavbar()"
                    >
                        <span class="sr-only">Open main menu</span>
                        <svg
                            class="w-6 h-6"
                            aria-hidden="true"
                            fill="currentColor"
                            viewBox="0 0 20 20"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                fill-rule="evenodd"
                                d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
                                clip-rule="evenodd"
                            ></path>
                        </svg>
                    </button>
                </div>
                <div v-bind:class="{ hidden: !showMenu, flex: showMenu }"
                     class="w-full lg:flex justify-between max-lg:bg-white py-5 max-lg:mt-1 max-lg:px-4 max-lg:shadow-lg max-lg:shadow-gray-200 max-lg:h-auto max-lg:overflow-auto transition-all duration-500 delay-200 "
                     id="navbar">
                    <ul
                        class="flex lg:items-center max-lg:gap-4 max-lg:mb-4 flex-col mt-4 lg:flex-1 md:mt-0 lg:flex-row"
                    >
                        <li class="text-gray-500 text-sm font-medium hover:text-prime-blue-700 transition-all duration-500 mb-2 block lg:mr-6 lg:text-base md:mb-0 md:mr-3 hover:text-gray-900">
                            <svg
                                version="1.1"
                                id="Layer_1"
                                xmlns="http://www.w3.org/2000/svg"
                                xmlns:xlink="http://www.w3.org/1999/xlink"
                                x="0px"
                                y="0px"
                                width="31.06px"
                                height="30.16px"
                                viewBox="0 0 31.06 30.16"
                                style="enable-background:new 0 0 31.06 30.16;"
                                xml:space="preserve"
                            >
                              <g>
                                <path
                                    style="fill:#5FECFD;"
                                    d="M7.62,14.76l0.54,0.37l-7.4-4.97C0.29,9.84,0.01,9.31,0.01,8.75L0,1.11C0,0.22,0.99-0.3,1.73,0.19l13.8,9.26 L7.62,14.76z"
                                />
                                  <path
                                      style="opacity:0.4; fill:#0147DC;"
                                      d="M22.86,15.15l-6.54,4.41c-0.23,0.16-0.51,0.24-0.78,0.24c0.26-0.01,0.52-0.08,0.74-0.23L22.86,15.15z"
                                  />
                                  <polygon
                                      style="fill:#0046D9;"
                                      points="23.44,14.76 15.53,9.45 16.59,8.74"
                                  />
                                  <path
                                      style="fill:#0153FF;"
                                      d="M31.06,1.11l-0.01,7.63c0,0.57-0.28,1.1-0.75,1.41l-6.86,4.6l0,0l-6.85-6.02l12.74-8.55 C30.07-0.3,31.06,0.22,31.06,1.11z"
                                  />
                                  <path
                                      style="fill:#00BDF7;"
                                      d="M23.44,14.76l-0.58,0.39l-6.57,4.41c-0.22,0.15-0.48,0.23-0.74,0.23h-0.02c-0.26-0.01-0.52-0.08-0.74-0.23 l-6.61-4.44l-0.54-0.37l7.91-5.31L23.44,14.76z"
                                  />
                                  <path
                                      style="opacity:0.4; fill:#0147DC;"
                                      d="M14.78,19.56c0.22,0.15,0.48,0.23,0.74,0.23c-0.27,0-0.54-0.08-0.78-0.24l-6.58-4.43L14.78,19.56z"
                                  />
                                  <polygon
                                      style="opacity:0.4; fill:#0147DC;"
                                      points="23.44,14.76 22.86,15.15 23.44,14.76"
                                  />
                                  <path
                                      style="fill:#0153FF;"
                                      d="M7.08,25.84c-2.01,1.4-4.03,2.8-6.04,4.2C0.6,30.34,0,30.03,0,29.49v-8.34c0-0.51,0.57-0.82,1-0.54l6.07,4.02 C7.5,24.92,7.51,25.55,7.08,25.84z"
                                  />
                                  <path
                                      style="fill:#5FECFD;"
                                      d="M31.06,21.15v8.34c0,0.54-0.6,0.85-1.04,0.54c-2.01-1.4-4.03-2.8-6.04-4.2c-0.42-0.29-0.42-0.92,0.01-1.21 l6.07-4.02C30.49,20.33,31.06,20.64,31.06,21.15z"
                                  />
                              </g>
                            </svg>
                        </li>
                        <li>
                            <Link
                                class="text-gray-500 text-sm font-medium hover:text-prime-blue-700 transition-all duration-500 mb-2 block lg:mr-6 lg:text-base md:mb-0 md:mr-3 hover:text-gray-900"
                                href="/">Home
                            </Link>
                        </li>
                        <li>
                            <Link
                                class="text-gray-500 text-sm font-medium hover:text-prime-blue-700 transition-all duration-500 mb-2 block lg:mr-6 lg:text-base md:mb-0 md:mr-3 hover:text-gray-900"
                                href="/products">Products
                            </Link>
                        </li>
                    </ul>

                    <div
                        class="flex lg:items-center justify-start flex-col lg:flex-row max-lg:gap-4 lg:flex-1 lg:justify-end">
                        <a
                            @click="toggleCart()"
                            class="px-3 py-2 flex items-center text-xs uppercase font-bold leading-snug text-blue-500 hover:opacity-75"
                            href="#"
                        >
                            <span class="mx-3 relative flex"
                            ><svg
                                class="h-8 w-8 flex-shrink-0 text-blue-800 group-hover:text-primary"
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
                                <span
                                    v-if="totalCartItems > 0"
                                    class="bg-green-100 custom-notification text-blue-800 absolute right-0 text-xs font-medium mr-2 px-2.5 py-0.5 rounded-full dark:bg-blue-800 dark:text-white"
                                >{{ totalCartItems }}</span
                                >
                            </span>
                        </a>


                        <Link :href="route('login')">
                            <button v-if="!$page.props.auth.user"
                                    class="bg-indigo-50 text-indigo-600 rounded-full cursor-pointer font-semibold text-center shadow-xs transition-all duration-500 py-3 px-6 text-sm hover:bg-indigo-100"
                            >
                                Login
                            </button>
                        </Link>

                        <Link :href="route('register')">
                            <button v-if="!$page.props.auth.user"
                                    class="bg-indigo-600 text-white rounded-full cursor-pointer font-semibold text-center shadow-xs transition-all duration-500 py-3 px-6 text-sm lg:ml-5 hover:bg-indigo-700"
                            >
                                Sign up
                            </button>
                        </Link>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>
<style scoped>
.custom-notification {
    position: absolute;
    padding: 3px;
    bottom: -10px;
    right: -20px;
}
</style>
