<script setup>
import Checkbox from "@/Components/Atoms/Checkbox.vue";
import InputError from "@/Components/Atoms/InputError.vue";
import InputLabel from "@/Components/Atoms/InputLabel.vue";
import PrimaryButton from "@/Components/Atoms/PrimaryButton.vue";
import TextInput from "@/Components/Atoms/TextInput.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";
import BlankLayout from "@/Layouts/BlankLayout.vue";

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: "",
    password: "",
    remember: false,
});

const submit = () => {
    form.post(route("login"), {
        onFinish: () => form.reset("password"),
    });
};
</script>

<template>
        <section class="flex justify-center relative">
            <div class="mx-auto max-w-lg px-6 lg:px-8 absolute py-20">
                <Link href="/">
                    <svg
                        class="w-20 h-20 mx-auto lg:mb-11 mb-6"
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
                <div class="rounded-2xl bg-white shadow-xl">
                    <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
                        {{ status }}
                    </div>
                    <form @submit.prevent="submit" class="lg:p-11 p-7 mx-auto">
                        <div class="mb-11">
                            <h1 class="text-gray-900 text-center font-manrope text-3xl font-bold leading-10 mb-2">Welcome Back</h1>
                            <p class="text-gray-500 text-center text-base font-medium leading-6">login here</p>
                        </div>


                        <input
                            id="email"
                            type="email"
                            class="w-full h-12 text-gray-900 placeholder:text-gray-400 text-lg font-normal leading-7 rounded-full border-gray-300 border shadow-sm focus:outline-none px-4 mb-6"
                            v-model="form.email"
                            required
                            autofocus
                            autocomplete="username"
                            placeholder="Enter your email"
                        />
                        <InputError class="mt-2" :message="form.errors.email" />

                        <input
                            id="password"
                            type="password"
                            class="w-full h-12 text-gray-900 placeholder:text-gray-400 text-lg font-normal leading-7 rounded-full border-gray-300 border shadow-sm focus:outline-none px-4 mb-6"
                            v-model="form.password"
                            required
                            autocomplete="current-password"
                            placeholder="Password"
                        />
                        <InputError class="mt-2" :message="form.errors.password" />
                        <Link
                            v-if="canResetPassword"
                            :href="route('password.request')"
                            class="flex justify-end mb-6"
                        >
                            <span class="text-indigo-600 text-right text-base font-normal leading-6">Forgot Password?</span>
                        </Link>

                        <button
                            class="w-full h-12 text-white text-center text-base font-semibold leading-6 rounded-full hover:bg-indigo-800 transition-all duration-700 bg-indigo-600 shadow-sm mb-11"
                            :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing"
                        >
                            Log in
                        </button>
                        <Link href="/register" class="flex justify-center text-gray-900 text-base font-medium leading-6"> Don’t have an account? <span class="text-indigo-600 font-semibold pl-3"> Sign Up</span>
                        </Link>
                    </form>
                </div>
            </div>
        </section>
</template>
