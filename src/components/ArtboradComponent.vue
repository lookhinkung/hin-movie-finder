<script lang="ts">
export default {
  props: {
    imgSrc: String,
    movieName: String,
    movieGroup: String,
    releaseYear: Number,
    // leadActors: (actors: string | null): string[] => {
    //   if (typeof actors === "string") {
    //     return actors.split(",");
    //   } else {
    //     return [""];
    //   }
    // },
    leadActors: String,
    ranking: Number,
    to: Number,
    prev: Number,
  },
  methods: {
    trimStr(str: string) {
      let trimmed = str.trim();
      return trimmed;
    },
  },
};
</script>
<script setup lang="ts">
import { ref } from "vue";
import LoadingComponent from "./LoadingComponent.vue";

const count = {
  likes: ref(0),
  dislikes: ref(0),
};
</script>
<template>
  <div v-if="imgSrc === ''" class="animate-pulse artboard artboard-demo">
    <LoadingComponent></LoadingComponent>
    <template> </template>
  </div>
  <div
    v-else
    class="rounded-xl duration-300 w-full artboard flex md:phone-1 lg:phone-1 xl:phone-3"
  >
    <img
      :src="imgSrc"
      class="hovering-artborad duration-300 basis-1/4 h-full w-full"
    />
    <div class="basis-3/4 flex flex-col gap-4 custom-font mx-6 mt-6">
      <h1 class="text-5xl break-words">{{ movieName }}</h1>
      <div class="flex gap-4">
        <p class="badge badge-primary badge-lg dynamic-text">
          <i class="fa-solid fa-tv fa-sm mr-2"></i>
          {{ movieGroup || "SHOWS" }}
        </p>
        <p class="badge bg-primary-focus badge-primary badge-lg dynamic-text">
          <i class="fa-regular fa-clock fa-sm mr-2"></i>
          {{ releaseYear || "2002" }}
        </p>
      </div>
      <div class="">
        <p class="badge badge-accent badge-lg dynamic-text">
          <i class="fa-solid fa-user-group fa-sm mr-2"></i>lead actors
        </p>
        <ul
          v-if="leadActors && leadActors.split(',').length == 2"
          class="flex flex-col gap-2 mt-2 ml-4"
        >
          <li
            class="badge dynamic-text text-slate-200 badge-accent bg-accent-focus badge-md"
          >
            <i class="fa-solid fa-person fa-sm mr-2"></i>
            {{ leadActors.split(",")[0] }}
          </li>
          <li
            class="badge dynamic-text text-slate-200 badge-accent bg-accent-focus badge-md"
          >
            <i class="fa-solid fa-person-dress fa-sm mr-2"></i>
            {{ leadActors.split(",")[1] }}
          </li>
        </ul>
        <ul v-else class="flex flex-col gap-2 mt-2 ml-4">
          <li
            class="badge dynamic-text text-slate-200 badge-accent bg-accent-focus badge-md"
          >
            <i class="fa-solid fa-person fa-sm mr-2"></i>
            {{ "John Doe" }}
          </li>
          <li
            class="badge dynamic-text text-slate-200 badge-accent bg-accent-focus badge-md"
          >
            <i class="fa-solid fa-person-dress fa-sm mr-2"></i>
            {{ "Jane Doe" }}
          </li>
        </ul>
      </div>
    </div>

    <!--- Utilities -->
    <div
      id="icon"
      class="absolute group-hover/card:visible flex right-2 flex-col gap-3 text-dark top-4"
    >
      <div class="grid grid-cols-2 place-self-center gap-2">
        <div
          @click="count.likes.value++"
          class="icon-hover bg-base-200 flex flex-col justify-center items-center gap-2 !opacity-100 rounded-lg h-10 w-10"
        >
          <i class="fa fa-regular fa-heart fa-lg mt-2"></i>
          <div class="badge badge-xs p-0.5 badge-secondary -mt-0.5">
            +{{ count.likes }}
          </div>
        </div>
        <div
          @click="count.dislikes.value++"
          class="icon-hover bg-base-200 flex flex-col justify-center items-center gap-2 !opacity-100 rounded-lg h-10 w-10"
        >
          <i class="fa-solid fa-heart-crack fa-lg mt-2"></i>
          <div class="badge badge-xs p-0.5 -mt-0.5">+{{ count.dislikes }}</div>
        </div>
      </div>
      <div
        class="visible md:invisible flex gap-1 justify-self-end text-md badge badge-primary font-semibold text-white"
      >
        <i class="fa-solid fa-user fa-sm"></i>
        {{ movieName }}
      </div>
      <div class="relative h-96 w-full">
        <p
          class="relative bottom-0 -right-10 pr-9 pl-3 py-6 bg-warning font-bold rounded-full"
        >
          RANK #{{ ranking || 89 }}
        </p>
      </div>
    </div>
    <div
      class="absolute flex justify-between transform -translate-y-1/2 left-5 right-5 top-1/2"
    >
      <a
        :href="`#slide${prev}`"
        class="opacity-hover opacity-80 animate-bounce btn btn-circle"
        >❮</a
      >
      <a
        :href="`#slide${to}`"
        class="opacity-hover animate-bounce btn btn-circle"
        >❯</a
      >
    </div>
  </div>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
.custom-font {
  font-family: "Bebas Neue", cursive;
}

@tailwind components;

@layer components {
  .opacity-hover:hover {
    @apply !opacity-100;
  }

  .hovering-artborad:hover {
    @apply opacity-90 shadow-lg;
  }

  .icon-hover:hover {
    @apply !opacity-100 duration-500 shadow-md md:shadow-gray-400 shadow-slate-300 cursor-pointer;
  }

  .icon-hover:not(:hover) {
    @apply duration-500;
  }

  .dynamic-text {
    @apply !text-sm md:!text-base lg:!text-lg;
  }
}
</style>
