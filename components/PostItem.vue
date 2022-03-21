<template>
  <Title> Articles | {{ title }} </Title>
  <div class="post-container  space-y-8 bg-white rounded rounded-xl shadow-lg px-5 py-8" v-for="article in articles"
       :key="article.id">
    <h3 class="text-3xl font-bold">
      <nuxt-link :to="`https://www.postimees.ee/${article.id}`">{{ article.headline }}</nuxt-link>
    </h3>

    <div class="post-meta text-gray-700 flex items-center space-x-2">
      <div> {{ (new Date(article.datePublished)).toLocaleString('lv') }}</div>
      <div>&middot;</div>
      <div> {{ article.authors.map(author => author.name).join(', ') }}</div>
    </div>
    <img class="object-contain" v-bind:src="article.editorsChoice.thumbnail.sources.landscape.medium">
    <div class="post-preview leading-relaxed mt-4" v-html="article.articleLead[0].html"></div>
    <div class="mt-4">
      <NuxtLink :to="`https://www.postimees.ee/${article.id}`" class="bg-blue-700 hover:bg-blue-800 text-white rounded
inline-block px-4 py-2"> Read More
      </NuxtLink>
    </div>
  </div>
</template>


<script setup>

const articles = ref([])

onMounted(() => {
  fetch('https://services.postimees.ee/rest/v1/sections/81/editorsChoice/articles?limit=5')
      .then(response => response.json())
      .then(data => articles.value = data)
})
const {data} = await useAsyncData('count', () => $fetch('https://services.postimees.ee/rest/v1/sections/81/editorsChoice/articles?limit=5'))
const title = useState('title')


</script>
