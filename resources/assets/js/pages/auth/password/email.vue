<template>
  <div class="row">
    <div class="col-lg-8 col-lg-offset-2">
      <div class="panel panel-default">
        <div class="panel-heading">
          {{ $t('login') }}
        </div>
        <div class="panel-body">
          <form @submit.prevent="send" @keydown="form.onKeydown($event)">
            <alert-success :form="form" :message="status"></alert-success>
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
                <v-button :loading="form.busy">{{ $t('reset_password') }}</v-button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Form from 'vform'

export default {
  metaInfo () {
    return { title: this.$t('reset_password') }
  },

  data: () => ({
    status: '',
    form: new Form({
      email: ''
    })
  }),

  methods: {
    async send () {
      const { data } = await this.form.post('/api/password/email')

      this.status = data.status

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
