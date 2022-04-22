<template>
    <div class="dice-throw" @click="emitClick">
        <svg viewBox="0 0 100 100" height="100%">
            <rect
                x="1"
                y="1"
                width="98"
                height="98"
                stroke="black"
                stroke-width="0.05rem"
                fill="white"
            />
            <text
                x="50%"
                y="50%"
                dominant-baseline="central"
                text-anchor="middle"
                font-size="5rem"
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
