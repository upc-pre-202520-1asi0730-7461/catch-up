<script setup lang="js">

import {computed, onMounted, ref} from "vue";
import {Menubar as PvMenubar} from "primevue";
import LanguageSwitcher from "./language-switcher.vue";
import FooterContent from "./footer-content.vue";
import {newsStore} from "../../../news/application/news.store.js";
import SourceList from "../../../news/presentation/components/source-list.vue";
import ArticleList from "../../../news/presentation/components/article-list.vue";

const drawerVisible = ref(false);
const toggleDrawer = () => {
  drawerVisible.value = !drawerVisible.value;
};

const sources = computed(() => newsStore.sources);
const errors = computed(() => newsStore.errors);
let articles = computed(() => newsStore.articles);
const rerenderKey = ref(0);
const setSource = source => {
  newsStore.setCurrentSource(source);
  articles = computed(() => newsStore.articles);
  rerenderKey.value += 1;
  toggleDrawer();
}

onMounted(() => {
  newsStore.loadSources();
  articles = computed(() => newsStore.articles);
  rerenderKey.value += 1;
})

</script>

<template>
  <div>
    <div>
      <pv-menubar>
        <template #start>
          <pv-button icon="pi pi-bars" label="CatchUp" text @click="toggleDrawer"/>
          <source-list v-model:sources="sources"
                       v-model:visible="drawerVisible"
                       v-on:source-selected="setSource($event)"/>
        </template>
        <template #end>
          <language-switcher></language-switcher>
        </template>
      </pv-menubar>
    </div>
  </div>
  <div>
    <article-list v-if="articles.length > 0" v-model:articles="articles" :key="rerenderKey"/>
  </div>
  <footer-content></footer-content>
</template>

<style scoped>

</style>