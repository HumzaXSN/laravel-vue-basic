<template>
  <div>
    Home Page User : {{ $auth.user.name }}
    <div>
      <Todo />
    </div>
  </div>
</template>

<script>
import Todo from "../components/Todo.vue";
export default {
    auth: true,
    name: "IndexPage",
    components: { Todo }
}
</script>
