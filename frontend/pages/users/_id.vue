<template>
  <div class="container mx-auto mt-16 ">
    <div class="flex space-x-6 mx-auto">
      <div class="flex flex-col items-end w-1/3">
        <h2 class="text-3xl">{{ user.name }}</h2>
        <template v-if="this.$auth.user.id != this.user.id">
          <form>
            <button type="submit">

            </button>
          </form>
        </template>
      </div>
      <div class="flex border-l mt-3 w-2/3">
        <div class="flex mb-3 ml-3">
          <img src="https://images.unsplash.com/photo-1506508839781-65d2a514b73a?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MzB8fGFub255bW91cyUyMHNpaG91ZXR0ZSUyMHdhbGxwYXBlcnxlbnwwfHwwfHw%3D&auto=format&fit=crop&w=500&q=60"
            alt="User Avatar" class="w-8 h-8 rounded-full object-cover">
            <div class="flex flex-col">
              <span class="text-xl ml-2">{{ user.name }}</span>
              <span class="text-xl ml-2">{{ user.email }}</span>
              <span class="text-xl ml-2">{{ user.created_at }}</span>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data:() => ({
      user: {},
    }),
    created() {
      this.getUser()
    },
    methods: {
      async getUser() {
        this.$axios.$get('/api/users/' + this.$route.params.id)
          .then((response) => {
            console.log(response);
            this.user = response;
          })
          .catch((error) => {
            console.log(error);
          });
      }
    }
  }
</script>
