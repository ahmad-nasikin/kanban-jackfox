<template lang="html">
  <div class="container">
    <div class="row master">
      <div class="row-1">
          <modal></modal><br>
      </div>
      <div class="row-2">
        <div class="col-md-3">
          <log></log>
        </div>
        <div class="col-md-3">
          <todo></todo>
        </div>
        <div class="col-md-3">
          <doing></doing>
      </div>
        <div class="col-md-3">
          <done></done>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import log from '@/components/Log'
import todo from '@/components/Todo'
import doing from '@/components/Doing'
import done from '@/components/Done'
import modal from '@/components/Modal'
export default {
  components: {
    log,
    todo,
    doing,
    done,
    modal
  }
}
</script>

<style lang="css">
</style>
