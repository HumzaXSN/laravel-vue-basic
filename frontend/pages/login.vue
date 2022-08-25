<template>
  <div class="mt-10 bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 flex flex-col">
    <form ref="loginform" @submit.prevent="login">
      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="email">
          Email
        </label>
        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker" id="email" type="email" placeholder="E-mail" name="email" required>
      </div>
      <div class="mb-6">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="password">
          Password
        </label>
        <input class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3" name="password" id="password" type="password" placeholder="******************" required>
        <p class="text-red text-xs italic">Please choose a password.</p>
      </div>
      <div class="flex items-center justify-between">
        <button class="p-2 bg-red-600 text-white rounded" type="submit">
          Sign In
        </button>
      </div>
    </form>
  </div>
</template>

<script>
  export default {
    auth: 'guest',
    mounted() {
      this.$axios.$get('/sanctum/csrf-cookie');
    },
    methods: {
      async login() {
        try {
          const formData = new FormData(this.$refs.loginform);
          await this.$auth.loginWith('laravelSanctum', { data: formData });
          console.log('login success');
          this.$router.push('/');
        } catch (error) {
          console.log(error);
        }
      }
    }
  }
</script>
