<template>
  <div>
    Dashboard Page User : {{ $auth.user.name }}, {{ $auth.user.email }}
    <div>
      <button type="button" class="bg-red-700 text-white rouded p-3" @click="logout">Logout</button>
    </div>
    <client-only>
      <div class="flex place-items-center px-40 py-7">
        <vue-good-table :columns="columns" :rows="todos" max-height="300px" :line-numbers="true" :search-options="{
         enabled: true,
         placeholder: 'Search...',
        }" :pagination-options="{
          enabled: true,
          perPage: 5,
          perPageDropdown: [5, 10, 15, 20, 25],
          position: 'bottom',
          align: 'center',
          style: {
            display: 'flex',
            justifyContent: 'center',
            alignItems: 'center',
            margin: '0 auto',
          },
          dropdownAllowAll: false,
        }" :select-options="{
          enabled: true,
        }" />
      </div>
    </client-only>
  </div>
</template>

<script>
  export default {
    middleware: 'auth',
    data() {
      return {
        columns: [
          {
            label: 'Content',
            field: 'content',
          },
          {
            label: 'Done OR Not',
            field: 'is_done',
          },
        ],
        todos: [],
      }
    },
    methods: {
      async logout() {
        await this.$auth.logout();
        this.$router.push('/login');
      },
    },
    async fetch() {
      try {
        const response = await this.$axios.$get('/api/todos');
        this.todos = response;
      } catch (error) {
        console.log(error);
      }
    },
  }
</script>
