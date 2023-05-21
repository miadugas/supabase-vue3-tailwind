<template>
  <div>

    <header class="w-full navbar bg-neutral text-neutral-content">
      <div class="navbar-start">
        <div class="dropdown">
          <label
            tabindex="0"
            class="btn btn-ghost btn-circle"
            @click="toggleDropdown"
          >
          <div>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
            >
              <path
                strokeLinecap="round"
                strokeLinejoin="round"
                strokeWidth="2"
                d="M4 6h16M4 12h16M4 18h7"
              />
            </svg>
            </div>
          </label>
          <ul
            v-show="isDropdownVisible"
            tabindex="0"
            class="menu menu-compact dropdown-content mt-3 p-2 shadow bg-base-100 rounded-box w-52 text-base-content"
          >
            <li><router-link to="/">Homepage</router-link></li>
            <li><router-link to="/">Portfolio</router-link></li>
            <li><router-link to="/">About</router-link></li>
          </ul>
        </div>
      </div>
      <div class="navbar-center">
        <p class="normal-case text-xl titleText">TrackMate</p>
      </div>
      <div class="navbar-end">
        <DarkLightToggle />
        <div class="dropdown dropdown-bottom dropdown-end">
          <label
            tabindex="0"
            class="btn btn-ghost btn-circle avatar"
            @click="toggleUserDropdown"
          >
            <div>
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="32"
                height="32"
                viewBox="0 0 16 16"
              >
                <path
                  fill="currentColor"
                  d="M8 8a3 3 0 1 0 0-6a3 3 0 0 0 0 6Zm2-3a2 2 0 1 1-4 0a2 2 0 0 1 4 0Zm4 8c0 1-1 1-1 1H3s-1 0-1-1s1-4 6-4s6 3 6 4Zm-1-.004c-.001-.246-.154-.986-.832-1.664C11.516 10.68 10.289 10 8 10c-2.29 0-3.516.68-4.168 1.332c-.678.678-.83 1.418-.832 1.664h10Z"
                />
              </svg>
            </div>
          </label>
          <ul
            v-show="isUserDropdownVisible"
            tabindex="0"
            class="mt-3 p-2 shadow menu menu-compact dropdown-content bg-base-100 rounded-box w-52 text-base-content"
          >
            <li>
              <a class="justify-between">Profile</a>
            </li>
            <li><a>Settings</a></li>
            <li><a @click="signOut">Logout</a></li>
          </ul>
        </div>
      </div>
    </header>
    <!-- OLD HEADER -->
    <!-- <header class="py-4 bg-gray-900">
      <div class="container flex items-center justify-between mx-auto p-2">
        <h1 class="text-lg font-bold text-white">Supabase DaisyUI</h1>
        <button
          class="w-auto px-4 py-2 font-semibold text-white bg-red-600 rounded hover:bg-red-700"
          @click="signOut"
        >
          Signout
        </button>
      </div>
    </header> -->
  </div>
</template>

<script setup>
import { supabase } from "@/supabase";
import { useAuth } from "@/composables/useAuth";
import { ref } from "vue";
import DarkLightToggle from "@/components/DarkLightToggle.vue";

useAuth();

const isDropdownVisible = ref(false);
const isUserDropdownVisible = ref(false);

const signOut = async () => {
  let { error } = await supabase.auth.signOut();
  if (!error) {
    window.location.href = "/";
  }
};
const toggleDropdown = () => {
  isDropdownVisible.value = !isDropdownVisible.value;
};
const toggleUserDropdown = () => {
  isUserDropdownVisible.value = !isUserDropdownVisible.value;
};
</script>
