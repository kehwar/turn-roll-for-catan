<template>
    <v-app>
        <v-app-bar app> Roll Turn for Catan </v-app-bar>
        <v-main>
            <v-container>
                <p>Who will play?</p>
                <div class="input">
                    <v-text-field
                        ref="textInput"
                        v-model="nameInput"
                        label="Player"
                        outlined
                        @keypress.enter="onEnter"
                    >
                    </v-text-field>
                    <v-btn @click="onEnter">Enter</v-btn>
                </div>
                <div class="chip-group">
                    <v-chip v-for="(name, index) in names" :key="index">
                        {{ name }}
                    </v-chip>
                </div>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
export default {
    name: 'IndexPage',
    data() {
        return {
            nameInput: '',
            names: [],
        }
    },
    methods: {
        onEnter() {
            if (this.nameInput === '') return
            this.names.push(this.nameInput)
            this.nameInput = ''
            this.$refs.textInput.focus()
        },
    },
}
</script>

<style scoped>
.input {
    display: flex;
    gap: 10px;
}
.chip-group {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}
</style>
