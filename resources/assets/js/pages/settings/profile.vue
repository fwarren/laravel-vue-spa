<template>
  <div class="panel panel-default">
    <div class="panel-heading">
      {{ $t('your_info') }}
    </div>
    <div class="panel-body">

      <form @submit.prevent="update" @keydown="form.onKeydown($event)">
        <alert-success :form="form" :message="$t('info_updated')"></alert-success>
  
        <!-- Name -->
        <div class="form-group row">
          <label class="col-md-3 col-form-label text-right">{{ $t('name') }}</label>
          <div class="col-md-7">
            <input v-model="form.name" type="text" name="name" class="form-control"
              :class="{ 'is-invalid': form.errors.has('name') }">
            <has-error :form="form" field="name"></has-error>
          </div>
        </div>
  
        <!-- Email -->
        <div class="form-group row">
          <label class="col-md-3 col-form-label text-right">{{ $t('email') }}</label>
          <div class="col-md-7">
            <input v-model="form.email" type="email" name="email" class="form-control"
              :class="{ 'is-invalid': form.errors.has('email') }">
            <has-error :form="form" field="email"></has-error>
          </div>
        </div>
  
        <!-- Submit Button -->
        <div class="form-group row">
          <div class="col-md-9 col-md-offset-3">
            <v-button type="success" :loading="form.busy">{{ $t('update') }}</v-button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Form from 'vform'
import { mapGetters } from 'vuex'

export default {
  data: () => ({
    form: new Form({
      name: '',
      email: ''
    })
  }),

  computed: mapGetters({
    user: 'authUser'
  }),

  created () {
    // Fill the form with user data.
    this.form.keys().forEach(key => {
      this.form[key] = this.user[key]
    })
  },

  methods: {
    async update () {
      const { data } = await this.form.patch('/api/settings/profile')

      this.$store.dispatch('updateUser', { user: data })
    }
  }
}
</script>

<style>
.invalid-feedback {
  color: #dc3545;
}
.is-invalid {
    border-color: #dc3545;
}
</style>
