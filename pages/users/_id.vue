<template>
  <section>
    <h1>{{ user.data.first_name }} {{ user.data.last_name }}</h1>
    <hr>
    <h3>
      {{ user.data.email }}
    </h3>
  </section>
</template>

<script>
export default {
  validate ({ params }) {
    return /^\d+$/.test(params.id)
  },
  async asyncData ({ $axios, params }) {
    const user = await $axios.$get('https://reqres.in/api/users/' + params.id)
    return { user }
  }
}
</script>
