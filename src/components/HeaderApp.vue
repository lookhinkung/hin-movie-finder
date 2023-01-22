<script lang="ts">
export default {
  props: [],
  data() {
    return {
      query: "",
    };
  },
  mounted() {
  },
  methods: {},
};
</script>
<script setup lang="ts">
import Swal from "sweetalert2";

const desc = `<div class="">
    <p class="font-mono text-warning xl:text-xl text-lg font-semibold">
      Playground
    </p>
    <ul
      class="ml-2 font-base lg:text-base text-sm text-yellow-600 break-words list-disc list-inside"
    >
      <li>Website tool ที่ช่วยหาภาพยนต์ที่ต้องการ</li>
      <li>ต้องทำการ Search หาภาพยนต์ก่อน ภาพยนต์ถึงจะถูกโหลดมาแสดงผล</li>
      <li>แต่ละภาพยนต์จะมีข้อมูลประกอบไปด้วย ชื่อ, ประเภทเรื่อง, วันที่ฉาย, นักแสดงนำ (ตัวเอก นางเอง) ปุ่มชอบ, ไม่ชอบ และ Ranking</li>
      <li>
        แต่ละภาพยนต์จะสามารถกดชอบ หรือ ไม่ชอบได้ซึ่งสามารถนับจำนวนรวมทั้งหมดได้
      </li>
      <li>สามารถ Search ภาพยนต์ได้ทุกเมื่อ (แต่จะจำกัดสิทธ์ 500 เรื่องต่อวัน)</li>
      <li>Responsive Layout on every screen size</li>
      <p class="font-mono text-blue-500 xl:text-xl text-lg font-semibold">
        API tools
      </p>
    </ul>
    <ul
      class="ml-2 font-base lg:text-base text-sm text-info break-words list-disc list-inside"
    >
      <li>ใช้ API จาก IMDB API ในการแสดงผลหนัง</li>
      <li>
        บางครั้งการตอน Query หาหนังจะมี Error เกิดขึ้นบ้างสาเหตุเนื่องจาก 1) หนังบางเรื่องที่ถูก Query ไม่มี
        รูปภาพมาด้วย จึงได้ตัดปัญหาด้วยการให้ Query ใหม่ 2) API เกิน Limit ที่กำหนด (500 per day)
      </li>
    </ul>
  </div>`;
const onShowInfo = () => {
  Swal.fire({
    title: "<h1>MovieFinder Application</h1>",
    html: desc,
    icon: "info",
    confirmButtonText: "OK",
    footer: `<h1 class="text-secondary text-lg">ทำโดย: นายติณณ์ ศรีสมศักดิ์ เลขนศ 6404101317</h1>`,
  });
};
onShowInfo();
</script>
<template>
  <div class="fixed top-0 z-10 navbar bg-base-300">
    <div class="flex-1">
      <a class="logo-font btn btn-ghost normal-case text-2xl"
        >Movies<u>Finder</u></a
      >
      <div class="flex-none">
        <button @click="onShowInfo" class="btn btn-square btn-ghost">
          <i class="fa-solid fa-bars fa-2xl"></i>
        </button>
      </div>
    </div>
    <div class="form-control mr-2">
      <input
        v-model="query"
        type="text"
        placeholder="Search"
        class="input input-bordered"
      />
    </div>
    <button
      @click="$emit('searchQuery', query)"
      class="btn btn-ghost btn-circle"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
        />
      </svg>
    </button>
  </div>
</template>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Pacifico&display=swap");
.logo-font {
  font-family: "Pacifico", cursive;
}
</style>
