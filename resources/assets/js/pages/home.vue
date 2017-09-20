<template>
  <div class="row">
    <div class="col-lg-8 col-lg-offset-2">
      <div class="panel panel-default">
        <div class="panel-heading">
          {{ $t('home') }}
        </div>
        <div class="panel-body">
          {{ $t('you_are_logged_in') }}
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  metaInfo () {
    return { title: this.$t('home') }
  }
}
</script>
