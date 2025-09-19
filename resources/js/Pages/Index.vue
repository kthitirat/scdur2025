<template>
  <Layout>
    <div class="p-4">
      <h1 class="text-3xl font-bold text-center">ยินดีต้อนรับสู่หน้าหลัก</h1>
    </div>
  </Layout>
</template>

<script>
import Layout from "@/Pages/Layout/Layout.vue";
import { Link, router } from "@inertiajs/vue3";
import axios from "axios";

export default {
  name: "Index",
  components: { Layout, Link },
};
</script>