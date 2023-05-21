<template>
  <div>
    <div class="text-center text-2xl font-bold leading-9 tracking-tight text-gray-900 titleText">Login</div>
    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
    <form class="px-8 pt-6 pb-8 mb-4 bg-white rounded shadow-xl">
      <div class="mb-4">
        <label
          class="block text-sm font-medium leading-6 text-gray-900"
          htmlFor="email"
        >
          Email
        </label>
        <input
        class="input input-primary input-bordered w-full"
          id="email"
          name="email"
          type="email"
          autocomplete="email"
          placeholder="Email"
          required=""
          v-model="state.email"
        />
      </div>
      <div class="mb-6">
        <label
          class="block mb-2 text-sm font-bold text-gray-700"
          htmlFor="password"
        >
          Password
        </label>
        <input
        class="input input-primary input-bordered w-full"
          id="password"
          type="password"
          placeholder="******************"
          v-model="state.password"
        />
      </div>
      <div class="items-center justify-between ">
        <button class="btn btn-primary btn-wide text-white" type="button" @click="login">
          Login
        </button>
      </div>
    </form>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";
import { supabase } from "@/supabase";

const state = reactive({
  loading: false,
  disabled: false,
  error: undefined,
  email: "miadugas@outlook.com",
  password: "1234",
});

const login = async () => {
  let { data, error } = await supabase.auth.signInWithPassword({
    email: state.email,
    password: state.password,
  });
};
</script>

<style lang="scss"></style>
