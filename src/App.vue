<script lang="ts">
import axios from "axios";
import Swal from "sweetalert2";
export default {
  data() {
    return {
      onLoading: false,
      movies: <any[]>[],
      errMsg: "",
      options: {
        method: "GET",
        url: "https://imdb8.p.rapidapi.com/auto-complete",
        params: { q: "" },
        headers: {
          "X-RapidAPI-Key":
            "84214a2573msh8eef85f0805fb7bp11f306jsn01780e8a3986",
          "X-RapidAPI-Host": "imdb8.p.rapidapi.com",
        },
      },
    };
  },
  emits: ["searchQuery"],
  methods: {
    onSearchQ(q: string) {
      this.options.params.q = q;
      (this.movies = <any[]>[]), (this.onLoading = true);
      const loadedPromise = new Promise((resolve) => {
        resolve(
          axios
            .request(this.options)
            .then((res) => {
              this.movies = res.data.d;
              console.log(this.movies);
            })
            .catch(function (error) {
              console.error(error);
            })
        );
      });
      loadedPromise
        .then(() => {
          for (let m of this.movies) {
            if (m["i"].imageUrl == null || m["i"].imageUrl == undefined) {
              return;
            }
          }
          this.onLoading = false;
          this.errMsg = "";
        })
        .catch(() => {
          this.errMsg = "Error occurs while resolving query! (ถ้าเกิดว่า เกิด error ติดต่อกันขณะ Query อาจเป็นเพราะ API เกิน Limit แล้วให้รอ Query วันใหม่ครับ)";
          Swal.fire({
            icon: "error",
            title: "Oops...",
            text: this.errMsg,
            footer: '<a class="text-lg text-primary">Please try again.</a>',
          });
          this.onLoading = false;
          this.errMsg = "";
        });
    },
  },
};
</script>

<script setup lang="ts">
import HeaderApp from "./components/HeaderApp.vue";
import ArtboardComponent from "./components/ArtboradComponent.vue";
import LoadingComponent from "./components/LoadingComponent.vue";
</script>

<template>
  <header>
    <HeaderApp @search-query="onSearchQ"></HeaderApp>
    <template> </template>
  </header>
  <main>
    <div class="container  mx-auto">
      <div
        v-if="onLoading === true"
        class="h-screen flex justify-center items-center"
      >
        <LoadingComponent></LoadingComponent>
      </div>

      <div v-else>
        <div class="carousel md:h-[80vh] h-auto flex items-center w-full my-20">
          <div
            :id="`slide${index}`"
            v-for="(m, index) in movies"
            class="rounded-xl shadow-xl carousel-item relative w-full bg-slate-300"
          >
            <ArtboardComponent
              :prev="index === 0 ? movies.length - 1 : index - 1"
              :to="index === movies.length - 1 ? 0 : index + 1"
              :img-src="m.i.imageUrl"
              :movie-name="m.l"
              :movie-group="m.q || null"
              :release-year="m.y || null"
              :lead-actors="m.s || null"
              :ranking="m.rank || null"
            ></ArtboardComponent>
          </div>
        </div>
        <div class="flex justify-center"></div>
      </div>
    </div>
  </main>
</template>

<style scoped></style>
