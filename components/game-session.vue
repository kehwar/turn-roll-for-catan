<template>
    <div class="game-session">
        <h1 class="current-player" @click="nextPlayer">
            {{ names[currentPlayer] }}
        </h1>
        <DiceThrow
            :number="diceThrow"
            class="dice-throw"
            @click="nextPlayer"
        ></DiceThrow>
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
        <v-btn x-large @click="nextPlayer">Next</v-btn>
        <v-btn x-small @click="gotoSetup">Setup</v-btn>
    </div>
</template>

<script>
import DiceThrow from './dice-throw.vue'
export default {
    components: { DiceThrow },
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
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.dice-throw {
    /* max-height: 50vh; */
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
</style>
