<template class="background">
  <Title> Articles | {{ title }} </Title>
  <div class="bg-cover bg-center h-96 flex items-center overlay heading ">
    <h3 class="text-3xl py-8 px-20 font-bold text-center">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Alias cupiditate et eveniet facilis placeat quo?
    </h3>
  </div>

  <div v-for="(article, index) in articles" :key="article.id">
    <div v-if="(index+1)%2!==0">
      <div class="bg-cover bg-center h-96 flex items-end overlay min-h-min"
           v-bind:style="{ backgroundImage: 'url(' +  article.editorsChoice.thumbnail.sources.landscape.large + ')'}">
        <h3 class="py-8 px-14 text-3xl font-bold">
          <nuxt-link :to="`https://www.postimees.ee/${article.id}`">{{ article.headline }}</nuxt-link>
        </h3>
      </div>

      <div class="flex min-h-min font-sans">
        <div class="w-3/4 bg-gray-700 py-6 pl-14 pr-8 text" v-html="article.articleLead[0].html"></div>
        <div class="w-1/4 lightBlue flex justify-center items-center">
          <div class="border w-20 h-20 rounded-full flex justify-center items-center text-lg">
            {{ index + 1 }}
          </div>
        </div>
      </div>
    </div>

    <div v-if="(index+1)%2===0">
      <div class="bg-cover bg-center h-96 flex items-end overlay"
           v-bind:style="{ backgroundImage: 'url(' +  article.editorsChoice.thumbnail.sources.landscape.large + ')'}">
        <h3 class="py-8 px-14 text-5xl font-bold">
          <nuxt-link :to="`https://www.postimees.ee/${article.id}`">{{ article.headline }}</nuxt-link>
        </h3>
      </div>

      <div class="flex">
        <div class="w-1/4 lightBlue flex justify-center items-center">
          <div class="border w-20 h-20 rounded-full flex justify-center items-center text-lg">
            {{ index + 1 }}
          </div>
        </div>
        <div class="w-3/4 bg-gray-700 py-6 pl-14 pr-8 text-lg" v-html="article.articleLead[0].html"></div>
      </div>
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

<style>
.overlay {
  color: white;
  background: -moz-linear-gradient(0deg, rgb(0, 0, 0) 0%, rgba(0, 0, 0, 0.18039) 100%), url("https://f12.pmo.ee/L69Sy466BKkxzGW7FT7FJUfCqpg=/1920x1080/smart/nginx/o/2022/03/22/14440869t1ha348.jpg");
  background: -webkit-linear-gradient(0deg, rgb(0, 0, 0) 0%, rgba(0, 0, 0, 0.18039) 100%), url("https://f12.pmo.ee/L69Sy466BKkxzGW7FT7FJUfCqpg=/1920x1080/smart/nginx/o/2022/03/22/14440869t1ha348.jpg");
  background-size: cover;
}

.lightBlue {
  background-color: #44bff2;
}

.heading {
  width: 100%;
  color: white;
  background: -moz-linear-gradient(0deg, rgb(0, 0, 0) 0%, rgba(0, 0, 0, 0.18039) 100%), url("assets/header-img.jpg");
  background: -webkit-linear-gradient(0deg, rgb(0, 0, 0) 0%, rgba(0, 0, 0, 0.18039) 100%), url("assets/header-img.jpg");
  background-size: cover;
}


</style>


