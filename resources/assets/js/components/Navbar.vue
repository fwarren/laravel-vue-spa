<template>
<nav class="navbar navbar-default">
  <div class="container">
    <!-- Brand and toggle get grouped for better mobile display -->
    <div class="navbar-header">
      <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" 
        data-target="#navbarToggler" aria-controls="navbarToggler"
        aria-expanded="false" :aria-label="$t('toggle_navigation')"
      >
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>

      <router-link :to="{ name: 'welcome' }" class="navbar-brand">
       {{ appName }}
      </router-link>
    </div>

    <!-- Collect the nav links, forms, and other content for toggling -->
    <div class="collapse navbar-collapse" id="navbarToggler">
      <!-- left hand side of navbar -->
      <ul class="nav navbar-nav">
        <!-- <li><a href="#">Link</a></li> -->
      </ul>

      <!-- right hand side of navbar -->
      <ul class="nav navbar-nav navbar-right">
        <!-- Authenticated -->
        <template v-if="authenticated">
          <router-link :to="{ name: 'settings.profile' }" tag="li" class="nav-item">
            <a class="nav-link">
              {{ user.name }}
            </a>
          </router-link>
          <li class="nav-item">
            <a @click.prevent="logout" href="#" class="nav-link">
              {{ $t('logout') }}
            </a>
          </li>
        </template>
        <!-- Guest -->
        <template v-else>
          <li class="nav-item">
            <router-link :to="{ name: 'login' }" class="nav-link" active-class="active">
              {{ $t('login') }}
            </router-link>
          </li>
          <li class="nav-item">
            <router-link :to="{ name: 'register' }" class="nav-link" active-class="active">
              {{ $t('register') }}
            </router-link>
          </li>
        </template>
      </ul>
    </div>
  </div>
</nav>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  data: () => ({
    appName: window.config.appName
  }),

  computed: mapGetters({
    user: 'authUser',
    authenticated: 'authCheck'
  }),

  methods: {
    async logout () {
      // Log out the user.
      await this.$store.dispatch('logout')

      // Redirect to login.
      this.$router.push({ name: 'login' })
    }
  }
}
</script>

<style scoped>
.navbar {
  border: 1px solid #d3e0e9;
}
</style>
