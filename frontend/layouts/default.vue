<template>
  <div>
    <div class="p-2 bg-gray-600 text-white">
      <NuxtLink class="p-2 bg-red-600 text-white rounded" v-if="$auth.loggedIn == true" to="/">HOME</NuxtLink>
      <NuxtLink class="p-2 bg-red-600 text-white rounded" v-if="$auth.loggedIn != true" to="/login">Login</NuxtLink>
      <NuxtLink class="p-2 bg-red-600 text-white rounded" v-if="$auth.loggedIn != true" to="/register">Register</NuxtLink>
      <NuxtLink class="p-2 bg-red-600 text-white rounded" v-if="$auth.loggedIn == true" to="/dashboard">Dashboard
      </NuxtLink>
    </div>
    <Nuxt />
  </div>
</template>
<script>
  export default {
    auth: false
  }
</script>
