<template>
    <div style="height: 100%">
        <PlayerSetup v-show="state === 'setup'" @play="startPlay"></PlayerSetup>
        <GameSession
            v-if="state === 'play'"
            :names="names"
            @setup="gotoSetup"
        ></GameSession>
    </div>
</template>

<script>
import GameSession from '~/components/game-session.vue'
import PlayerSetup from '~/components/player-setup.vue'
export default {
    name: 'IndexPage',
    components: { PlayerSetup, GameSession },
    data() {
        return {
            names: ['AAAAA', 'BBBB'],
            state: 'play',
        }
    },
    methods: {
        startPlay(names) {
            this.names = names
            this.state = 'play'
        },
        gotoSetup() {
            this.state = 'setup'
        },
    },
}
</script>
