<template>

  <div class="text-xl mx-8 sm:mx-10 my-14 sm:my-10 leading-loose">

    <div class="my-10">Explore the untold stories of Pakistan's
      
      <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 64 64" class="inline mx-1"><path fill="#e6e7e8" d="M10 10C3.373 10 0 14.925 0 21v22c0 6.075 3.373 11 10 11h10V10z"/><path fill="#006838" d="M54 10H20v44h34c6.627 0 10-4.925 10-11V21c0-6.075-3.373-11-10-11"/><g fill="#e6e7e8"><path d="m44.509 21.528l2.264 2.101l3.01-.671l-1.298 2.806l1.57 2.66l-3.073-.374l-2.044 2.319l-.593-3.03l-2.84-1.231l2.7-1.506z"/><path d="M52.37 35.33c-4.301 4.302-11.272 4.302-15.574 0c-4.302-4.301-4.302-11.273 0-15.574c.297-.296.607-.567.927-.822a12.638 12.638 0 0 0-5.829 3.312c-4.966 4.967-4.966 13.02 0 17.987c4.969 4.966 13.02 4.966 17.987 0a12.638 12.638 0 0 0 3.312-5.829a11.48 11.48 0 0 1-.823.926"/></g></svg>
      
      unsung heroes. <span class="underline underline-offset-8">Miras</span> is a tribute to the individuals who have made significant contributions to our nation, often <u class="underline-offset-8 decoration-wavy">without recognition</u>.</div>

    <div v-for="hero in formattedData" :key=hero.title  class="inline-flex">
      <NuxtLink :to="hero.path"><div class="m-2 sm:mx-4 sm:my-4 hover:underline decoration-wavy underline-offset-8"><Icon name="lucide:arrow-up-right"></Icon><div class="inline p-1"></div>{{ hero.title }}</div></NuxtLink>
    </div>

    <div class="my-10">Do you know someone hasn't received the recognition they deserve? At Miras, we believe that every hero's story deserves to be told. We invite you to share the stories of these remarkable individuals.</div>
  </div>
</template>

<script lang="ts" setup>

const { data } = await useAsyncData('home', () => queryContent('/heroes').sort({ _id: 1 }).find())

const formattedData = computed(() => {
  return data.value?.map((articles) => {
    return {
      path: articles._path,
      title: articles.title || 'no-title available',
      description: articles.description || 'no-description available',
      tags: articles.tags || [],
    }
  }) || []
})

</script>

<style>

</style>