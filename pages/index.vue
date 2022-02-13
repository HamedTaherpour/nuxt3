<template>
  <NuxtLayout name="custom">
    <div class="flex flex-col px-4 h-full overflow-y-auto">
      <div
        class="flex-none flex flex-row my-2 border border-gray-200 rounded overflow-hidden"
        v-for="user in data"
        :key="user.id"
      >
        <div>
          <img class="w-32 h-32" :src="user.avatar_url" />
        </div>
        <div class="flex flex-col pl-2 justify-center">
          <h2 class="text-lg font-bold" v-text="user.login"></h2>
          <div class="mt-5 flex flex-row justify-between items-center">
            <a class="text-gray-400" :href="user.html_url">
              <svg
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
                ></path>
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  layout: false,
  async setup() {
    const { data } = await useAsyncData("users", () =>
      $fetch("https://api.github.com/users")
    );

    return { data };
  },
});
</script>
