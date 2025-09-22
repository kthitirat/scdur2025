<template>
 <Layout>
    <div class="mx-auto max-w-7xl px-4 pt-0 pb-4">
      <!-- มือถือ: ดันสไลด์ให้กว้างเท่าหน้าจอ, เดสก์ท็อปยังอยู่ใน max-w -->
      <div class="relative w-screen left-1/2 -ml-[50vw] sm:w-auto sm:left-auto sm:ml-0">
        <HeroSlider :slides="slides" :intervalMs="5500" />
      </div>

    </div>
  </Layout>
</template>

<script>
import Layout from "@/Pages/Layout/Layout.vue";
import HeroSlider from "@/Components/HeroSlider.vue";

export default {
  name: "Index",
  components: { Layout, HeroSlider },
  data() {
    return {
      slides: [
        {
          image: "/images/1.png",         
        },
      ],
    };
  },
};
</script>
