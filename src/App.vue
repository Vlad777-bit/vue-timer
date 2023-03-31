<script setup>
import { ref } from 'vue';
import MyTimer from './components/MyTimer.vue';

let id = 0;

const timers = ref([
    { id: id++, timerId: 0, paused: true, hours: 0, minutes: 0, seconds: 0 },
]);

const addTimer = () => {
    timers.value = [
        ...timers.value,
        {
            id: id++,
            timerId: 0,
            paused: true,
            hours: 0,
            minutes: 0,
            seconds: 0,
        },
    ];
};

const startTimer = (timer) => {
    timer.timerId = setTimeout(function run() {
        if (timer.seconds < 60) {
            ++timer.seconds;
        } else if (timer.minutes < 60) {
            timer.seconds = 0;
            ++timer.minutes;
        } else {
            timer.seconds = 0;
            timer.minutes = 0;
            ++timer.hours;
        }

        timer.timerId = setTimeout(run, 1000);
    }, 1000);

    timer.paused = false;
};

const resetTimer = (timer) => {
    clearTimeout(timer.timerId);

    timer.seconds = 0;
    timer.minutes = 0;
    timer.hours = 0;

    timer.paused = true;
};

const stopTimer = (timer) => {
    clearTimeout(timer.timerId);

    timer.paused = true;
};
</script>

<template>
    <div class="container">
        <MyTimer
            v-for="timer in timers"
            :key="timer.id"
            :paused="timer.paused"
            :hours="timer.hours"
            :minutes="timer.minutes"
            :seconds="timer.seconds"
            @start="startTimer(timer)"
            @stop="stopTimer(timer)"
            @reset="resetTimer(timer)"
        />

        <button @click="addTimer">
            <span></span>
        </button>
    </div>
</template>

<style scoped lang="scss">
.container {
    width: 1024px;

    margin: 0 auto;
    padding: 72px 20px;

    display: grid;
    grid-template-columns: repeat(3, 255px);
    grid-template-rows: 120px;
    grid-auto-rows: 120px;
    justify-content: center;
    align-items: center;
    gap: 50px;

    button {
        height: 100%;

        background: none;
        border: none;
        cursor: pointer;
        background-color: #696969;
    }

    span {
        display: inline-block;
        width: 3em;
        height: 3em;

        background: linear-gradient(#9e9e9e, #9e9e9e),
            linear-gradient(#9e9e9e, #9e9e9e);
        background-position: center;
        background-size: 50% 3px, 3px 50%;
        background-repeat: no-repeat;
    }
}

@media (max-width: 1024px) {
    .container {
        width: auto;
    }
}

@media (max-width: 903px) {
    .container {
        grid-template-columns: repeat(2, 255px);
    }
}

@media (max-width: 768px) {
    .container {
        grid-template-columns: repeat(2, 255px);
    }
}

@media (max-width: 603px) {
    .container {
        grid-template-columns: 255px;
    }
}
</style>
