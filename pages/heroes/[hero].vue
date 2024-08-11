<script setup lang="ts">

import type { Hero } from '~/types/hero';

const { path } = useRoute()

const { data: articles, error } = await useAsyncData(`blog-post-${path}`, () => queryContent(path).findOne())

if (error.value) navigateTo('/404')

const data = computed<Hero>(() => {
  return {
    title: articles.value?.title || 'no-title available',
    description: articles.value?.description || 'no-description available',
    tags: articles.value?.tags || [],
    wikipedia: articles.value?.wikipedia
  }
})

definePageMeta({
  layout: 'default'
})

</script>

<template>
  <div class="flex justify-center items-center md:p-20 p-10 text-lg leading-loose text-justify">
    <div class="md:w-[60%] space-y-6 prose-a:underline underline-offset-8">

      <div class="flex justify-between"><div class="text-2xl underline decoration-wavy underline-offset-8">{{ data.title }}</div><a :href= data.wikipedia><Icon name="mdi:wikipedia" size="36px"></Icon></a></div>

      <ContentRenderer v-if="articles" :value="articles">
        <template #empty>
          <p>No content found.</p>
        </template>
      </ContentRenderer>
    </div>
  </div>  
</template>

<style scoped>
/* Ensure that the content is centered both vertically and horizontally */
.min-h-screen {
  min-height: 100vh;
}
</style>
