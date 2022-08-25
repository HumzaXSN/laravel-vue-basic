<template>
  <div class=" mt-10 bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 flex flex-col">
    <form ref="registerform" @submit.prevent="register">
      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="email">
          Email
        </label>
        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker" id="email" type="email"
          placeholder="E-mail" name="email" required>
      </div>
      <div class="mb-4">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="name">
          Name
        </label>
        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker" id="name" type="text"
          placeholder="Name" name="name" required>
      </div>
      <div class="mb-6">
        <label class="block text-grey-darker text-sm font-bold mb-2" for="password">
          Password
        </label>
        <input class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3"
          name="password" id="password" type="password" placeholder="******************" required>
        <p class="text-red text-xs italic">Please choose a password.</p>
      </div>
      <div class="flex items-center justify-between">
        <button class="p-2 bg-red-600 text-white rounded" type="submit">
          Sign In
        </button>
        <!-- <a class="inline-block align-baseline font-bold text-sm text-blue hover:text-blue-darker" href="#">
          Forgot Password?
        </a> -->
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
      async register() {
        try {
          const formData = new FormData(this.$refs.registerform);
          this.$axios.post('/register', formData).then(response => {
            this.$auth.loginWith('laravelSanctum', { data: formData });
            console.log('login success');
            this.$router.push('/');
          });
        } catch (error) {
          console.log(error);
        }
      }
    }
  }
</script>
