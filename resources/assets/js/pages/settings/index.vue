<template>
  <div class="row">
    <div class="col-md-3">
      <div class="panel panel-default settings-card">
        <div class="panel-heading">
          {{ $t('settings') }}
        </div>
        <div class="panel-body">
          <ul class="nav nav-pills nav-stacked">
            <li v-for="tab in tabs" class="nav-item">
              <router-link :to="{ name: tab.route }" class="nav-link" active-class="active">
                <icon :name="tab.icon"></icon>
                {{ tab.name }}
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="col-md-9">
      <transition name="fade" mode="out-in">
        <router-view></router-view>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  loading: false,

  data () {
    return {
      tabs: [
        {
          icon: 'user',
          name: this.$t('profile'),
          route: 'settings.profile'
        },
        {
          icon: 'lock',
          name: this.$t('password'),
          route: 'settings.password'
        }
      ]
    }
  }
}
</script>

<style>
.settings-card .card-body {
  padding: 0;
}
</style>
