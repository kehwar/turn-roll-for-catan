<template>
    <div class="game-session">
        <h1 class="current-player" @click="nextPlayer">
            {{ names[currentPlayer] }}
        </h1>
        <BigDice
            :number="diceThrow"
            class="dice-throw"
            :surface-color="colors[diceHistory.length % 2]"
            :on-surface-color="colors[(diceHistory.length + 1) % 2]"
            @click="nextPlayer"
        ></BigDice>
        <div class="buttons">
            <v-btn
                class="next-button"
                x-large
                color="#F2C335"
                @click="nextPlayer"
                >Next</v-btn
            >
            <v-btn class="home-button" x-large @click="gotoSetup">
                <v-icon>mdi-home</v-icon>
            </v-btn>
        </div>
        <div
            v-show="diceHistory.length > 0"
            ref="diceHistory"
            class="dice-history"
        >
            <span
                v-for="(dice, index) in diceHistory"
                :key="index"
                :style="'--index:' + index"
            >
                {{ dice }}
            </span>
        </div>
    </div>
</template>

<script>
import BigDice from './big-dice.vue'
export default {
    components: { BigDice },
    props: {
        names: {
            type: Array,
            required: true,
        },
    },
    data() {
        return {
            diceThrow: 0,
            currentPlayer: 0,
            diceHistory: [],
            colors: ['#F2C438', '#BF2431'],
        }
    },
    mounted() {
        this.throwDice()
    },
    methods: {
        throwDice() {
            this.diceThrow = this.getOneDiceRoll() + this.getOneDiceRoll()
        },
        getOneDiceRoll() {
            return Math.floor(Math.random() * 6 + 1)
        },
        nextPlayer() {
            // Change current player
            if (this.currentPlayer < this.names.length - 1)
                this.currentPlayer += 1
            else this.currentPlayer = 0
            // Save dice history
            this.saveDiceHistory()
            // Throw new dice
            this.throwDice()
        },
        saveDiceHistory() {
            this.diceHistory.splice(0, 0, this.diceThrow)
            this.$refs.diceHistory.scrollTo({ left: 0, behavior: 'smooth' })
        },
        gotoSetup() {
            this.$emit('setup')
        },
    },
}
</script>

<style scoped>
h1 {
    text-align: center;
    user-select: none;
}

.game-session {
    display: flex;
    flex-direction: column;
    height: 100%;
    gap: 1rem;
}

.dice-history {
    display: flex;
    gap: 10px;
    overflow-x: auto;
}

.dice-history > span {
    --color: hsl(0, 0%, min(50%, calc(10% + (var(--index) * 20%))));
    flex: none;
    border: 1px solid var(--color);
    display: flex;
    width: 3rem;
    height: 3rem;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
    user-select: none;
    color: var(--color);
}

.buttons {
    display: flex;
    width: 85%;
    align-self: center;
    gap: 1rem;
}

.buttons > .next-button {
    flex-grow: 1;
}
</style>
