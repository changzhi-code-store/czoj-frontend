<template>
  <div id="basic-layout">
    <a-layout style="height: 400px">
      <a-layout-header class="header">
        <GlobalHeader />
      </a-layout-header>
      <a-layout-content class="content">
        <router-view />
      </a-layout-content>
      <a-layout-footer class="footer">
        <a href="http://yupi.icu" target="_blank">Operation @ cz-OJ by 长志</a>
      </a-layout-footer>
    </a-layout>
  </div>
</template>

<style>
#basic-layout .content {
  background: linear-gradient(to right, #aaa, #fff);
  padding: 20px;
}

#basic-layout .footer {
  background: #ccc;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
  padding: 10px;
}
</style>
<script setup lang="ts">
import GlobalHeader from "@/components/GlobalHeader.vue";
</script>
