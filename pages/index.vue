<template>
    <v-app>
        <v-app-bar app> Roll Turn for Catan </v-app-bar>
        <v-main>
            <v-container>
                <div v-if="state === 'setup'">
                    <h1>Player Setup</h1>
                    <div class="input">
                        <v-text-field
                            ref="textInput"
                            v-model="nameInput"
                            label="Player"
                            outlined
                            clearable
                            hide-details=""
                            @keypress.enter="onEnter"
                        >
                        </v-text-field>
                        <v-btn x-large @click="onEnter">Enter</v-btn>
                    </div>
                    <div class="players">
                        <h2 v-if="names.length > 0">Players</h2>
                        <div class="player-chips">
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
                    </div>
                    <v-btn
                        x-large
                        :disabled="names.length === 0"
                        @click="startPlay"
                        >Play</v-btn
                    >
                </div>
                <div v-if="state === 'play'">
                    <h1 class="current-player">{{ names[currentPlayer] }}</h1>
                    <span class="dice-throw">{{ diceThrow }}</span>
                    <div class="dice-history">
                        <span v-for="(dice, index) in diceHistory" :key="index">
                            {{ dice }}
                        </span>
                    </div>
                    <v-btn x-large @click="nextPlayer">Next</v-btn>
                    <v-btn x-small @click="state = 'setup'">Setup</v-btn>
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
            names: ['', ''],
            state: 'setup',
            diceThrow: 0,
            currentPlayer: 0,
            diceHistory: [],
        }
    },
    methods: {
        onEnter() {
            if (this.nameInput === '') return
            this.names.push(this.nameInput)
            this.nameInput = ''
            this.$refs.textInput.focus()
        },
        removePlayer(index) {
            this.names.splice(index, 1)
        },
        startPlay() {
            this.currentPlayer = 0
            this.diceHistory = []
            this.throwDice()
            this.state = 'play'
        },
        nextPlayer() {
            if (this.currentPlayer < this.names.length - 1)
                this.currentPlayer += 1
            else this.currentPlayer = 0
            this.throwDice()
        },
        throwDice() {
            this.diceHistory.splice(0, 0, this.diceThrow)
            this.diceThrow = this.throwOneDice() + this.throwOneDice()
        },
        throwOneDice() {
            return Math.floor(Math.random() * 6 + 1)
        },
    },
}
</script>

<style scoped>
h1,
h2 {
    text-align: center;
}

.container {
    height: 100%;
}

.container > div {
    display: flex;
    flex-direction: column;
    gap: 20px;
    max-width: 500px;
    margin: auto;
    justify-content: flex-start;
    height: 100%;
    align-content: center;
}

.input {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}

.players {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.player-chips {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
}

.dice-throw {
    border: 1px solid black;
    display: flex;
    flex: 1 1 0;
    justify-content: center;
    align-content: center;
    align-items: center;
    font-weight: bold;
    font-size: 10rem;
}

.dice-history {
    display: flex;
    gap: 10px;
    overflow: scroll;
}

.dice-history > span {
    border: 1px solid black;
    display: flex;
    width: 40px;
    height: 40px;
    justify-content: center;
    align-content: center;
    align-items: center;
    flex: none;
}
</style>
