<template>
  <section>
    <h1>Users page</h1>
    <ul>
      <li
        v-for="user in users.data"
        :key="user.id"
      >
        <a @click.prevent="openUser(user)" href="#">
          {{ user.id }} {{ user.first_name }} {{ user.last_name }}
        </a>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  // data: () => ({
  //   users: []
  // }),
  computed: {
    users () {
      return this.$store.getters['users/users']
    }
  },
  async fetch ({ store }) {
    if (store.getters['users/users'].length === 0) {
      await store.dispatch('users/fetch')
    }
  },
  methods: {
    openUser (user) {
      this.$router.push('/users/' + user.id)
    }
  }
}
</script>
