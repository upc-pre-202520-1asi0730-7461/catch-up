<script setup lang="js">
import ArticleItem from "./article-item.vue";
import {Article} from "../../domain/model/article.entity.js";

const props = defineProps({ articles: { type: Array[Article], required: true } });
  const { articles } = props;
</script>

<template>
  <div v-for="article in articles">
    <article-item :article="article"/>
  </div>
</template>

<style scoped>

</style>