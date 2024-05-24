<template>
    <div class="app">
        <BrasilMap />
    </div>
</template>

<script>
import BrasilMap from './components/layout/BrasilMap.vue'

export default {
    components: {
        BrasilMap
    },

    setup() {



        return {

        }
    }
}
</script>

<style scoped>
.app {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #222
}
</style>