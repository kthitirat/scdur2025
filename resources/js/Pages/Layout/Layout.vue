<template>
  <div class="min-h-screen">
    <Nav />
    <section id="content"
             class="text-gray-800 z-0 px-4 md:px-8 lg:px-10 xl:px-16 min-h-screen
                    pt-[60px] md:pt-[220px] lg:pt-[240px]">
      <main>
        <slot></slot>
      </main>
    </section>
    <Footer />
  </div>
</template>

<script>
import Nav from "@/Pages/Layout/Nav.vue";
import Footer from "@/Pages/Layout/Footer.vue";

export default {
  name: "Layout",
  components: { Footer, Nav },
};
</script>

<style scoped>

</style>