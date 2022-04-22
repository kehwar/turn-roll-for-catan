<template>
    <v-app>
        <v-main>
            <v-container fluid>
                <Nuxt></Nuxt>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
export default { name: 'DefaultLayout' }
</script>

<style scoped>
/* v-container class */
.container {
    max-width: 40rem;
    height: 100%;
}
</style>
