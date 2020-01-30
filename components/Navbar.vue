<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Nuxt SSR</a>

    <div class="collapse navbar-collapse">
      <ul class="navbar-nav mr-auto">
        <li
          v-for="item in menuLinks"
          :key="item.id"
          class="nav-item"
        >
          <n-link
            :to="item.link"
            exact
            active-class="active"
            class="nav-link"
            no-prefetch
          >
            {{ item.name }}
          </n-link>
        </li>
        <li
          v-if="!hasToken"
          class="nav-item"
        >
          <n-link
            to="/login"
            exact
            class="btn btn-outline-success"
            no-prefetch
          >
            Login
          </n-link>
        </li>
        <li
          v-else
          class="nav-item"
        >
          <a
            @click.prevent="logout"
            href="#"
            class="btn btn-outline-danger"
          >
            Logout
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navbar',
  data: () => ({
    menuLinks: [
      {
        id: 1,
        name: 'Home',
        link: '/'
      },
      {
        id: 2,
        name: 'About',
        link: '/about'
      },
      {
        id: 3,
        name: 'Users',
        link: '/users'
      }
    ]
  }),
  computed: {
    hasToken () {
      return this.$store.getters.hasToken
    }
  },
  methods: {
    logout () {
      this.$store.dispatch('logout')
      this.$router.push('/login')
    }
  }
}
</script>
