<template>
  <div class=" min-h-screen text-white">
    <nav class="py-6 px-4 flex items-center justify-between">
      <div>
        <NuxtLink to="/"><img src="~/assets/logo.png/"/></NuxtLink>
      </div>

      <div class="flex items-center justify-between space-x-8">
        <div class="flex items-center justify-between space-x-2">
          <NuxtLink :to="`${ Object.keys(contact).length === 0 ? '' : contact.meta.social.facebook }`"><img
              src="~/assets/facebook.png/"/>
          </NuxtLink>
          <NuxtLink :to="`${ Object.keys(contact).length === 0 ? '' : contact.meta.social.twitter }`"><img
              src="~/assets/twitter.png/"/>
          </NuxtLink>
          <NuxtLink :to="`${ Object.keys(contact).length === 0 ? 'loading' : contact.editor.email }`"><img
              src="~/assets/email.png/"/>
          </NuxtLink>
          <img src="~/assets/comments.png/"/>
          <p> 88 </p>
        </div>

        <div>
          <NuxtLink to="/">Login</NuxtLink>
        </div>
      </div>
    </nav>

    <slot/>
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
nav {
  background-color: #0064FA;
  color: white;
}
</style>
