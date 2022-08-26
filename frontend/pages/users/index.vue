<template>
  <div class="container mx-auto mt-16">
    <div class="flex space-x-6 mx-auto w-1/2">
      <h2 class="flex-shrink-0 text-3xl">Users</h2>
      <div class="flex-1 border-l mt-3">
        <div v-for="user in users" :key="user.id" class="flex mb-3 ml-3">
          <img src="https://images.unsplash.com/photo-1506508839781-65d2a514b73a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzB8fGFub255bW91cyUyMHNpaG91ZXR0ZSUyMHdhbGxwYXBlcnxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60"
            alt="User Avatar" class="w-8 h-8 rounded-full object-cover">
          <NuxtLink :to="`/users/${user.id}`" class="text-xl ml-2">{{ user.name }}</NuxtLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data:() => ({
      users: []
    }),
    mounted() {
      this.getUsers();
    },
    methods: {
      async getUsers() {
        try {
          const response = await this.$axios.$get('/api/users');
          this.users = response;
        } catch (error) {
          console.log(error);
        }
      }
    },
  }
</script>
