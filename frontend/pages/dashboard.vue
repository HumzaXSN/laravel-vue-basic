<template>
  <div class="font-bold">
    Dashboard Page User : {{ $auth.user.name }}, {{ $auth.user.email }}
    <div>
      <button type="button" class="bg-red-700 text-white rouded p-3" @click="logout">Logout</button>
    </div>
  </div>
</template>

<script>
  export default {
    middleware: 'auth',
    methods: {
      async logout() {
        await this.$auth.logout();
        this.$router.push('/login');
      }
    }
  }
</script>
