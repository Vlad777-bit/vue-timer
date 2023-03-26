<script setup>
defineProps({
    paused: Boolean,

    hours: Number,
    minutes: Number,
    seconds: Number,
});

const emit = defineEmits({
    start: null,
    stop: null,
    reset: null,
});
</script>

<template>
    <div :class="paused ? 'timer' : 'timer active'">
        <h2>
            {{ hours ? `${hours}:` : null }}{{ minutes ? `${minutes}:` : null
            }}{{ seconds }}
        </h2>

        <div class="timer__buttons">
            <button>
                <svg
                    v-if="paused"
                    @click="emit('start')"
                    width="17"
                    height="20"
                    viewBox="0 0 17 20"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <path d="M0 20V0L17 10L0 20Z" />
                </svg>

                <svg
                    v-else
                    @click="emit('stop')"
                    width="10"
                    height="20"
                    viewBox="0 0 10 20"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <rect x="7" width="3" height="20" />
                    <rect width="3" height="20" />
                </svg>
            </button>

            <button>
                <svg
                    @click="emit('reset')"
                    width="20"
                    height="20"
                    viewBox="0 0 20 20"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <rect width="20" height="20" />
                </svg>
            </button>
        </div>
    </div>
</template>

<style scoped lang="scss">
$not_active: #9e9e9e;
$active: #ffffff;

.timer {
    padding-top: 22px;

    height: 100%;

    display: flex;
    flex-direction: column;
    align-items: center;

    background-color: #696969;

    h2 {
        color: $not_active;

        // Text
        font-size: 22px;
        font-weight: 400;
        line-height: 21px;
    }

    &__buttons {
        margin-top: 20px;
        border-top: 1px solid $not_active;

        width: 100%;

        display: flex;
        justify-content: center;
        align-items: center;

        button {
            margin-top: 20px;

            background: none;
            border: none;
            cursor: pointer;

            &:not(:last-child) {
                margin-right: 45px;
            }
        }

        svg {
            fill: $not_active;
        }
    }
}

.active {
    h2 {
        color: $active;
    }

    .timer__buttons {
        border-top: 1px solid $active;

        svg {
            fill: $active;
        }
    }
}
</style>
