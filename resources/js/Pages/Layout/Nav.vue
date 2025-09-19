<template>
  <header class="fixed top-0 left-0 right-0 z-50">
    <!-- แถบริบบอน -->
    <div class="w-full bg-[#F3D798] h-10 flex items-center justify-center">
      <p class="text-[#7D5B29] text-sm md:text-base">
        Phranakhon Si Ayutthaya Rajabhat University
      </p>
    </div>

    <!-- แถวโลโก้ -->
    <div class="w-full bg-white shadow-md">
      <div class="container mx-auto max-w-7xl px-4 md:px-8 lg:px-32 py-2">
        <div class="flex items-center gap-4">
          <img src="/images/logo.png" alt="University Logo" class="h-16 md:h-20 lg:h-24" />
          <div class="flex flex-col text-center md:text-left">
            <p class="text-base md:text-xl lg:text-2xl font-bold">
              มหาวิทยาลัยกับการพัฒนาชุมชนอย่างยั่งยืน
            </p>
            <p class="text-xs md:text-sm lg:text-base text-gray-600">
              (Sustainable Community Development University Ranking: SCDUR)
            </p>
          </div>
        </div>
      </div>
    </div>

        <!-- แถวนำทาง -->
    <nav class="w-full bg-[#A54734] overflow-visible">
    <div class="container mx-auto max-w-7xl px-4 md:px-8 lg:px-32 h-12 md:h-16 flex items-center gap-4 md:gap-8">
        <Link :href="route('index')" class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap">หน้าหลัก</Link>
        <Link href="#" class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap">เกี่ยวกับหน่วยงาน</Link>

        <!-- Dropdown -->
        <div class="relative pt-2" @mouseenter="open = true" @mouseleave="scheduleClose()">
        <button
            type="button"
            class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap inline-flex items-center"
            :aria-expanded="open ? 'true' : 'false'"
            @click="open = !open">
            SCDUR 2023
            <svg class="h-4 w-4 inline-block ml-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
            </svg>
        </button>

        <!-- กล่องเมนู: ไม่มี mt-2, ใช้ transition + z สูง -->
        <div
            class="absolute left-0 top-full w-56 bg-[#A54734] text-white rounded-md shadow-lg py-2 z-[70]
                transition ease-out duration-150"
            :class="open ? 'opacity-100 translate-y-0 pointer-events-auto visible' : 'opacity-0 -translate-y-1 pointer-events-none invisible'">
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">ประวัติ</a>
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">เกณฑ์การประเมิน</a>
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">ผู้เข้าร่วม</a>
        </div>
        </div>

        <Link href="#" class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap">
        รายงานผล SCDUR2024
        </Link>
        <a href="https://example.com/announcements.pdf" target="_blank" class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap">
        ประกาศที่เกี่ยวข้อง
        </a>
        <Link href="#" class="text-white text-xs md:text-sm lg:text-base hover:text-gray-200 whitespace-nowrap">
        ติดต่อเรา
        </Link>
    </div>
    </nav>
  </header>
</template>

<script>
import { Inertia } from "@inertiajs/inertia";
import { Link } from "@inertiajs/vue3";

export default {
  name: "Nav",
  components: { Link },
  data() {
    return {
        isMenuOpen: false,
        open: false, 
        closeTimer: null
    };
  },
  methods: {
    logout() {
      Inertia.post(this.route('logout'));
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    scheduleClose() { this.closeTimer = setTimeout(()=> this.open = false, 150) },
    cancelClose() { if (this.closeTimer) clearTimeout(this.closeTimer) }
  },
};
</script>

<style scoped>
/* ไม่ต้องใช้ .mt-40/.md:mt-52/.lg:mt-56 อีกต่อไป */
</style>
