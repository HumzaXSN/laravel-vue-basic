<template>
  <div class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0">
    <div class="w-full">
      <div class="h-100 w-full flex items-center justify-center bg-teal-lightest font-sans">
        <div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
            <div class="mb-4">
              <h1 class="font-bold text-3xl text-gray-600 text-center">Todo List</h1>
              <div class="flex mt-4">
                <input class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"
                  placeholder="Add Todo" v-model="content" name="content">
                <button
                  class="flex-no-shrink p-2 border-2 rounded-lg text-teal border-teal text-white bg-blue-500 hover:bg-blue-700"
                  @click="submit">Add</button>
              </div>
            </div>
            <div>
              <div class="flex mb-4 items-center" v-for="(todo, i) in todos" :key="todo.id">
                <p :class="[todo.is_done ? 'line-through text-green-600' : '', `w-full text-grey-darkest font-semibold text-gray-600`]">{{ todo.content }}</p>
                <button @click="updateStatus(todo, i)" v-if="todo.is_done"
                  class="flex-no-shrink w-1/3 p-2 ml-4 mr-2 border-2 rounded-lg border-grey">Not Done</button>
                <button @click="updateStatus(todo, i)" v-else
                  class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded-lg border-green text-white bg-green-500 hover:bg-green-700">Done</button>
                <button @click="deleteTodo(todo, i)"
                  class="flex-no-shrink p-2 ml-2 border-2 rounded-lg text-red border-red text-white bg-red-500 hover:bg-red-700">Remove</button>
              </div>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
 data() {
    return {
      todos: [],
      content: ''
    }
  },
  methods: {
    submit: function() {
      this.$nuxt.$loading.start();
      this.$axios.post('/api/todos', {
        content: this.content
      }).then((response) => {
        this.todos.push(response.data)
        this.content = ''
      }).catch((error) => {
        console.log(error)
      }).finally(() => {
        this.$nuxt.$loading.finish();
      });
    },
    updateStatus: function(todo, i) {
      this.$nuxt.$loading.start();
      let api = '/api/todos/' + todo.id
      this.$axios.put(api).then((response) => {
        this.todos[i].is_done = response.data.is_done
      }).catch((error) => {
        console.log(error);
      }).finally(() => {
        this.$nuxt.$loading.finish();
      });
    },
    deleteTodo: function(todo, i) {
      this.$nuxt.$loading.start();
      let api = '/api/todos/' + todo.id
      this.$axios.delete(api).then((response) => {
        this.todos.splice(i, 1);
      }).catch((error) => {
        console.log(error);
      }).finally(() => {
        this.$nuxt.$loading.finish();
      });
    }
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
