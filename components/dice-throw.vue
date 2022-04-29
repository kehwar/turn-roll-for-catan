<template>
    <div class="dice-throw" @click="emitClick">
        <svg viewBox="0 0 100 100" width="100%">
            <rect
                x="1"
                y="1"
                width="98"
                height="98"
                :stroke="onSurfaceColor"
                stroke-width="0.05rem"
                :fill="surfaceColor"
            />
            <text
                x="50%"
                y="50%"
                dominant-baseline="central"
                text-anchor="middle"
                font-size="5rem"
                :fill="onSurfaceColor"
                stroke="white"
                stroke-width="0.025rem"
            >
                {{ number }}
            </text>
        </svg>
    </div>
</template>

<script>
export default {
    props: {
        number: {
            type: Number,
            required: true,
        },
        surfaceColor: {
            type: String,
            default: '#FFFFFF',
        },
        onSurfaceColor: {
            type: String,
            default: '#000000',
        },
    },
    methods: {
        emitClick() {
            this.$emit('click')
        },
    },
}
</script>

<style scoped>
svg {
    pointer-events: none;
    user-select: none;
}

.dice-throw {
    margin-inline: auto;
}
</style>
