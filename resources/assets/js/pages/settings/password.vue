<template>
  <div class="panel panel-default">
    <div class="panel-heading">
      {{ $t('your_password') }}
    </div>
    <div class="panel-body">
      <form @submit.prevent="update" @keydown="form.onKeydown($event)">
        <alert-success :form="form" :message="$t('password_updated')"></alert-success>
  
        <!-- Password -->
        <div class="form-group row">
          <label class="col-md-3 col-form-label text-right">{{ $t('new_password') }}</label>
          <div class="col-md-7">
            <input v-model="form.password" type="password" name="password" class="form-control"
              :class="{ 'is-invalid': form.errors.has('password') }">
            <has-error :form="form" field="password"></has-error>
          </div>
        </div>
  
        <!-- Password Confirmation -->
        <div class="form-group row">
          <label class="col-md-3 col-form-label text-right">{{ $t('confirm_password') }}</label>
          <div class="col-md-7">
            <input v-model="form.password_confirmation" type="password" name="password_confirmation" class="form-control"
              :class="{ 'is-invalid': form.errors.has('password_confirmation') }">
            <has-error :form="form" field="password_confirmation"></has-error>
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

export default {
  data: () => ({
    form: new Form({
      password: '',
      password_confirmation: ''
    })
  }),

  methods: {
    async update () {
      await this.form.patch('/api/settings/password')

      this.form.reset()
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
