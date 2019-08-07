<template>
    <div v-if="track && track.album"  class="card">
        <div class="card-image">
           <figure class="image .is-1by1">
               <img v-bind:src="track.album.images[0].url">
           </figure>
        </div>

        <div class="card-contend">
            <div class="media">
                <div class="media-left">
                    <figure class="image is-48x48">
                        <img v-bind:src="track.album.images[0].url">
                    </figure>
                </div>

                <div class="media-content">
                    <p class="title is-6">
                        <strong>{{ track.name }}</strong>
                    </p>
                    <p class="subtitle is-6">
                        {{ track.artists[0].name}}
                    </p>
                </div>
            </div>

             <div class="content has-text-centered">
                <small>{{ track.duration_ms | ms-to-mm }}</small>
                <nav class="level">
                    <div class="level-item has-text-centered">
                        <button class="level-item button is-primary">
                            <span class="icon is-small " v-on:click="selectTrack" >
                                Play
                            </span>
                        </button>

                        <button class="level-item button is-warning">
                            <span class="icon is-small " v-on:click="goToTrack(track.id)" >
                                Más
                            </span>
                        </button>
                    </div>
                </nav>
            </div>

           
        </div>
    </div>
</template>


<script>
export default {
    props: {
        track: { type: Object, required: true }
    },

    methods: {
        selectTrack(){
            if(!this.track.preview_url) { return }
            
            this.$emit('select', this.track.id)
            
            this.$bus.$emit('set-track', this.track)
        },
        goToTrack(id){
            if(!this.track.preview_url) { return }

            this.$router.push({ name: 'track', params: {id : id} })
        }
    }
}
</script>

<style lang="scss" scoped>
    .level-item{
        padding: 10px 20px;
    }
</style>
