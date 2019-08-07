<template>
    <section class="hero is-success">
        <div class="hero-head">
            <header class="navbar">
                <div class="container">
                    <div class="navbar-start">
                        <div class="navbar-item">
                            <strong>PreMusify</strong>
                        </div>
                    </div>
                    <div class="navbar-end .navbar-menu">
                        <router-link class="navbar-item" to="/">Buscar</router-link>
                        <router-link class="navbar-item" to="about">Nosotros</router-link>
                    </div>
                </div>
            </header>
        </div>

        <div class="hero-body">
            <div class="container has-text-centered">
                <h1 class="title">PreMusify</h1>
                <h2 class="subtitle">Busca canciones <stron class="has-text-dark">Vue</stron>nísimas</h2>
                <pm-player></pm-player>
            </div>
        </div>
    </section>
</template>


<script>
    import PmPlayer from '@/components/Player.vue'

    export default {
        components: { PmPlayer }
    }
</script>
