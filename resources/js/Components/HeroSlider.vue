<template>
<section class="relative w-full">
  <!-- เพิ่ม hero-ipad -->
  <div class="relative w-full overflow-hidden "
       @mouseenter="pause" @mouseleave="resume">

    <!-- ใส่คลาส frame ที่คอนเทนเนอร์สไลด์ -->
    <div v-if="count" class="relative w-full hero-frame">
    <div class="absolute inset-0 transition-transform duration-500 text-[0]"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
        <div v-for="(s, i) in safeSlides" :key="i" class="inline-block w-full h-full align-top">
        <div class="relative w-full h-full">
            <!-- สำคัญ: ตัด sm:object-cover ออก แล้วใช้คลาส hero-img -->
            <img
            :src="s.image" :alt="s.alt || ''"
            :loading="i===currentIndex ? 'eager' : 'lazy'"
            class="hero-img absolute inset-0 w-full h-full"
            />
        </div>
        </div>
    </div>
    </div>


    <div v-else class="w-full" style="padding-top:56.25%"></div>
  </div>
</section>
</template>

<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({
    // เดิม: required true → เปลี่ยนเป็นมีค่าเริ่ม []
    slides: { type: Array, default: () => [] },
    intervalMs: { type: Number, default: 5500 },
    })

    const currentIndex = ref(0)
    const playing = ref(true)
    let timer = null

    // กรองสไลด์ให้ปลอดภัย (มี object และมี image)
    const safeSlides = computed(() =>
    (Array.isArray(props.slides) ? props.slides : [])
        .filter(s => s && typeof s === 'object' && s.image)
    )

    const count = computed(() => safeSlides.value.length)

    function next(){
    if (!count.value) return
    currentIndex.value = (currentIndex.value + 1) % count.value
    }
    function prev(){
    if (!count.value) return
    currentIndex.value = (currentIndex.value - 1 + count.value) % count.value
    }
    function go(i){
    if (i >= 0 && i < count.value) currentIndex.value = i
    }
    function resume(){ playing.value = true }
    function pause(){ playing.value = false }

    function startTimer(){
    stopTimer()
    if (count.value > 1) {
        timer = setInterval(() => { if (playing.value) next() }, props.intervalMs)
    }
    }
    function stopTimer(){ if (timer) { clearInterval(timer); timer = null } }

    watch(safeSlides, (arr) => {
    if (currentIndex.value >= arr.length) currentIndex.value = 0
    startTimer()
    }, { immediate: true })

    onMounted(startTimer)
    onBeforeUnmount(stopTimer)
</script>


<style scoped>
/* สัดส่วน container ต่อจอ: ไม่ใช้ vh/min-h อีกต่อไป */
.hero-frame { aspect-ratio: 4 / 3; }                  /* mobile เป็น 4:3 ดูเต็มตา */
    @media (min-width: 768px){ .hero-frame { aspect-ratio: 16 / 9; } }   /* iPad */
    @media (min-width: 1280px){ .hero-frame { aspect-ratio: 21 / 9; } }  /* desktop กว้าง */

/* รูป: ให้เห็นครบ (ไม่ยืด/ไม่บี้) + กลืนกับพื้นการ์ดด้วยพื้นหลังขาว */
    .hero-img { object-fit: contain; object-position: center; background:#fff; }

/* ถ้าบางรูปต้องเลื่อนโฟกัสบน iPad นิดหน่อย (ไม่กระทบมือถือ/เดสก์ท็อป) */
@media (min-width: 768px) and (max-width: 1194px){
  .hero-img { object-position: center 20%; }  /* ปรับ 16–24% ตามภาพจริงได้ */
}
</style>
