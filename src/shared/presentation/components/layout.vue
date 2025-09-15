<script setup lang="js">

import {ref} from "vue";
import {Menubar as PvMenubar} from "primevue";
import LanguageSwitcher from "./language-switcher.vue";
import FooterContent from "./footer-content.vue";

const drawerVisible = ref(false);
const toggleDrawer = () => {
  drawerVisible.value = !drawerVisible.value;
};

</script>

<template>
  <div>
    <div>
      <pv-menubar>
        <template #start>
          <pv-button icon="pi pi-bars" label="CatchUp" text @click="toggleDrawer"/>
          <!-- TODO: Source List -->
        </template>
        <template #end>
          <language-switcher></language-switcher>
        </template>
      </pv-menubar>
    </div>
  </div>
  <div>
    <!-- TODO: Article List -->
  </div>
  <footer-content></footer-content>
</template>

<style scoped>

</style>