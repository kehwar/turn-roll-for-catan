<template>
    <div class="player-setup">
        <h1>Player Setup</h1>
        <div class="player-input">
            <v-text-field
                ref="textInput"
                v-model="inputValue"
                label="Player"
                outlined
                clearable
                hide-details=""
                @keypress.enter="addPlayer"
            >
            </v-text-field>
            <v-btn x-large @click="addPlayer">Enter</v-btn>
        </div>
        <h2 v-show="names.length > 0">Players</h2>
        <div v-show="names.length > 0" class="player-chips">
            <v-chip
                v-for="(name, index) in names"
                :key="index"
                close
                @click:close="removePlayer(index)"
                @dblclick="removePlayer(index)"
            >
                {{ name }}
            </v-chip>
        </div>
        <v-btn x-large :disabled="names.length < 2" @click="emitPlayEvent">
            Play
        </v-btn>
    </div>
</template>

<script>
export default {
    data() {
        return {
            inputValue: '',
            names: [],
        }
    },
    methods: {
        addPlayer() {
            if (this.inputValue === '') return
            this.names.push(this.inputValue)
            this.inputValue = ''
            this.$refs.textInput.focus()
        },
        removePlayer(index) {
            this.names.splice(index, 1)
        },
        emitPlayEvent() {
            this.$emit('play', this.names)
        },
    },
}
</script>

<style scoped>
h1,
h2 {
    text-align: center;
}

.player-setup {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    height: 100%;
}

.player-input {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}

.player-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
    justify-content: center;
}
</style>
