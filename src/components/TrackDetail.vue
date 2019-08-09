<template>
    <div class="container">
        <div class="columns">
            <div class="column is-3 has-text-centered">
                <figure class="media-left">
                  <p>
                    <img v-bind:src="track.album.images[0].url">
                  </p>
                  <p>
                    <a class="button is-primary is-fullwidth">
                      <span class="icon" v-on:click="selectTrack">Play</span>
                    </a>
                  </p>
                </figure>
            </div>

            <div class="column is-8">
              <div class="panel">
                <div class="panel-heading">
                  <h1 class="title">{{ track.name }}</h1>
                </div>
                <div class="panel-block">
                  <article class="media">
                    <div class="media-content">
                      <div class="content">
                        <ul>
                          <li>
                            <span><strong>Duración:</strong> {{ track.duration_ms | ms-to-mm }} min.</span>
                          </li>
                          <li>
                            <span><strong>Artistas:</strong> {{ track.artists[0].name }} {{ track.artists[1].name }} {{ track.artists[3].name }} </span>
                          </li>
                          <li>
                            <span><strong>Lanzamiento:</strong> {{ track.album.release_date }} </span>
                          </li>
                        </ul>
                      </div>

                      <nav class="level">
                        <div class="level-left">
                          <a class="level-item">

                          </a>
                        </div>
                      </nav>
                    </div>
                  </article>
                </div>
              </div>
            </div>
        </div>
    </div>
</template>

<script>
import trackService from '@/services/track'
import trackMixin from '@/mixins/track'

export default {
  mixins: [trackMixin],

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





