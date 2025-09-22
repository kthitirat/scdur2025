<template>
  <header ref="root" class="fixed top-0 left-0 right-0 z-50 bg-white">
    <!-- ริบบอน -->
    <div class="w-full bg-[#F3D798] h-9 sm:h-10 flex items-center justify-center">
      <p class="text-[#7D5B29] text-xs sm:text-sm md:text-base">
        Phranakhon Si Ayutthaya Rajabhat University
      </p>
    </div>

    <!-- โลโก้ + ชื่อเรื่อง -->
    <div class="w-full border-b border-gray-100">
      <div class="mx-auto max-w-7xl px-3 sm:px-4 md:px-8 lg:px-10 py-2">
        <div class="flex items-center gap-3 sm:gap-4">
          <img src="/images/logo.png" alt="University Logo" class="h-12 sm:h-16 md:h-20 lg:h-24" />
          <div class="flex-1 min-w-0">
            <p class="font-bold text-[#1f2937]" :style="{ fontSize: 'clamp(14px, 2.2vw, 28px)', lineHeight: 1.15 }">
              มหาวิทยาลัยกับการพัฒนาชุมชนอย่างยั่งยืน
            </p>
            <p class="hidden sm:block text-[11px] sm:text-xs md:text-sm lg:text-base text-gray-600">
              (Sustainable Community Development University Ranking: SCDUR)
            </p>
          </div>

          <!-- แฮมเบอร์เกอร์ (เฉพาะ < md) -->
          <button
            class="md:hidden inline-flex items-center justify-center w-10 h-10 rounded-md text-white bg-[#A54734] hover:bg-[#8D3B2C]"
            @click="mobileOpen = true" aria-label="Open menu">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-6 h-6" fill="none"
                 viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"/>
            </svg>
          </button>
        </div>
      </div>
    </div>

    <!-- เมนูเดสก์ท็อป -->
    <nav class="hidden md:block w-full bg-[#A54734]">
      <div class="mx-auto max-w-7xl px-4 md:px-8 lg:px-10 h-12 md:h-14 flex items-stretch gap-2">
        <Link :href="route('index')" :class="navLink">หน้าหลัก</Link>
        <Link href="#" :class="navLink">เกี่ยวกับหน่วยงาน</Link>

        <div class="relative" @mouseenter="open = true" @mouseleave="open = false">
          <button type="button" :class="navLink + ' gap-1'" @click="open = !open">
            SCDUR 2023
            <svg class="h-4 w-4 -mt-px" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
            </svg>
          </button>
          <div v-show="open" class="absolute left-0 top-full w-56 bg-[#A54734] text-white rounded-md shadow-lg py-2 z-[70]">
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">ประวัติ</a>
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">เกณฑ์การประเมิน</a>
            <a href="#" class="block px-4 py-2 hover:bg-[#8D3B2C]">ผู้เข้าร่วม</a>
          </div>
        </div>

        <Link href="#" :class="navLink">รายงานผล SCDUR2024</Link>
        <a href="#" target="_blank" :class="navLink">ประกาศที่เกี่ยวข้อง</a>
        <Link href="#" :class="navLink">ติดต่อเรา</Link>
      </div>
    </nav>

    <!-- เมนูมือถือแบบ Drawer -->
    <transition name="fade">
      <div v-if="mobileOpen" class="md:hidden fixed inset-0 z-[60]">
        <div class="absolute inset-0 bg-black/40" @click="mobileOpen = false"></div>
        <aside class="absolute left-0 top-0 bottom-0 w-[82%] max-w-sm bg-white shadow-xl">
          <div class="flex items-center justify-between px-4 py-3 border-b">
            <span class="font-semibold">เมนู</span>
            <button class="inline-flex items-center justify-center w-9 h-9 rounded-md text-white bg-[#A54734] hover:bg-[#8D3B2C]"
                    @click="mobileOpen = false" aria-label="Close menu">✕</button>
          </div>
          <nav class="px-2 py-2">
            <Link :href="route('index')" class="mobileItem">หน้าหลัก</Link>
            <Link href="#" class="mobileItem">เกี่ยวกับหน่วยงาน</Link>
            <details class="mobileDetails">
              <summary class="mobileItem">SCDUR 2023</summary>
              <div class="pl-4">
                <a href="#" class="mobileSub">ประวัติ</a>
                <a href="#" class="mobileSub">เกณฑ์การประเมิน</a>
                <a href="#" class="mobileSub">ผู้เข้าร่วม</a>
              </div>
            </details>
            <Link href="#" class="mobileItem">รายงานผล SCDUR2024</Link>
            <a href="#" target="_blank" class="mobileItem">ประกาศที่เกี่ยวข้อง</a>
            <Link href="#" class="mobileItem">ติดต่อเรา</Link>
          </nav>
        </aside>
      </div>
    </transition>
  </header>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from "vue";
import { Inertia } from "@inertiajs/inertia";
import { Link } from "@inertiajs/vue3";

export default {
  name: "Nav",
  components: { Link },
  setup() {
    const root = ref(null);
    let ro = null;

    const setHeaderHeightVar = () => {
      if (!root.value) return;
      const h = root.value.getBoundingClientRect().height;
      document.documentElement.style.setProperty("--header-h", `${Math.ceil(h)}px`);
    };

    onMounted(() => {
      setHeaderHeightVar();
      // อัปเดตเมื่อ header เปลี่ยนขนาด (รูปโหลด/ย่อ-ขยาย/เปลี่ยนทิศ)
      ro = new ResizeObserver(setHeaderHeightVar);
      ro.observe(root.value);
      window.addEventListener("orientationchange", setHeaderHeightVar);
      window.addEventListener("load", setHeaderHeightVar);
    });

    onBeforeUnmount(() => {
      if (ro) ro.disconnect();
      window.removeEventListener("orientationchange", setHeaderHeightVar);
      window.removeEventListener("load", setHeaderHeightVar);
    });

    return { root };
  },
  data() {
    return {
      open: false,
      mobileOpen: false,
      navLink:
        "inline-flex items-center h-full px-3 md:px-4 text-white text-sm md:text-base font-medium hover:text-gray-200"
    };
  },
  methods: { logout() { Inertia.post(this.route("logout")); } },
};
</script>

<style scoped>
.fade-enter-active, .fade-leave-active { transition: opacity .15s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.mobileItem { @apply block px-3 py-3 text-[#A54734] font-medium hover:bg-[#FFF3EF] rounded-md; }
.mobileSub  { @apply block px-3 py-2 text-[#6B7280] hover:text-[#A54734] rounded-md; }
.mobileDetails > summary { list-style: none; }
.mobileDetails > summary::-webkit-details-marker { display: none; }
</style>
