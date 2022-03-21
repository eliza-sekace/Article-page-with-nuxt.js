<template>
  <div class="bg-gray-100 min-h-screen text-gray-900">
    <nav class="bg-white shadow text-lg px-6 py-6">
      <div class="container mx-auto flex items-center justify-between px-6">
        <div>
          <NuxtLink to="/"><img src="https://f.pmo.ee//logos//81//c7d9ba40a7a5ec0fea7ab4a177b2005d.svg"/></NuxtLink>
        </div>
        <div>
              <NuxtLink to="/">Home</NuxtLink>
        </div>
      </div>
    </nav>

    <slot/>

    <footer>
      <div class="flex bg-white shadow text-lg py-6 items-center justify-between px-6 ">
        <div class="container mx-auto flex items-center justify-between px-6 space-x-2">
          <div class="flex space-x-2 ">
            <p> Editor: </p>
            <div> {{ Object.keys(contact).length === 0 ? 'loading' : contact.editor.name }}</div>
            <p>|</p>
            <div> {{ Object.keys(contact).length === 0 ? 'loading' : contact.editor.email }}</div>
          </div>

          <div class="flex space-x-10">
            <NuxtLink :to="`${ Object.keys(contact).length === 0 ? '' : contact.meta.social.facebook }`"><img
                src="~/assets/facebook.png/"/>
            </NuxtLink>
            <NuxtLink :to="`${ Object.keys(contact).length === 0 ? '' : contact.meta.social.twitter }`"><img
                src="~/assets/twitter.png/"/>
            </NuxtLink>
            <NuxtLink :to="`${ Object.keys(contact).length === 0 ? '' : contact.meta.social.instagram }`"><img
                src="~/assets/instagram.png/"/>
            </NuxtLink>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
const title = useState('title', () => 'Postimees')
const contact = ref({})
onMounted(() => {
  fetch('https://services.postimees.ee/rest/v1/sections/81')
      .then(response => response.json())
      .then(data => contact.value = data)
})
const {data} = await useAsyncData('count', () => $fetch('https://services.postimees.ee/rest/v1/sections/81'))
</script>

<style>
.router-link-active {
  font-weight: bold;
}
</style>
