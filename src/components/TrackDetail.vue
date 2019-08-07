<template>
    <div class="container">
        <div class="columns">
            <div class="column is-4 is-offset-4">
                <pm-track v-bind:track="track"></pm-track>
            </div>
        </div>
    </div>
</template>

<script>
import trackService from '@/services/track'
import PmTrack from '@/components/Track.vue'

export default {
  components: { PmTrack },

  data () {
    return {
      track: {}
    }
  },

  created () {
    const id = this.$route.params.id

    trackService.getById(id)
      .then(res => {
        this.track = res
      })
  }
}
</script>

<style lang="scss" scoped>
    .columns{
        margin: 20px;
    }
</style>


