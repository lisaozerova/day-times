<template>
  <h1>Выбирай время суток, Михаил</h1>

  <div class="multi-button">
    <button v-on:click="setDayTime(DayTime.MORNING)">Утро</button>
    <button v-on:click="setDayTime(DayTime.DAY)">День</button>
    <button v-on:click="setDayTime(DayTime.EVENING)">Вечер</button>
    <button v-on:click="setDayTime(DayTime.NIGHT)">Ночь</button>
  </div>

  <keep-alive>
    <component v-bind:is="dayTimeComponent" />
  </keep-alive>
</template>

<script>
import { computed, ref } from 'vue';

import Day from '@/components/Day';
import Evening from '@/components/Evening';
import Morning from '@/components/Morning';
import Night from '@/components/Night';
import DayTime from '@/enums/DayTime';

export default {
  name: 'App',

  components: {
    Day,
    Evening,
    Morning,
    Night,
  },

  setup() {
    const dayTime = ref(null);

    const dayTimeComponent = computed(() => {
      switch (dayTime.value) {
        case DayTime.MORNING:
          return Morning;
        case DayTime.DAY:
          return Day;
        case DayTime.EVENING:
          return Evening;
        case DayTime.NIGHT:
          return Night;
        default:
          return null;
      }
    });

    const setDayTime = dayTimeType => dayTime.value = dayTimeType;

    return {
      dayTime,
      DayTime,
      dayTimeComponent,
      setDayTime,
    }
  },
}
</script>

<style>
html,
body {
  height: 100%;
}


body {
  animation: gradient 15s ease infinite;
  background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
  background-size: 400% 400%;
  color: #2c3e50;
  font-family: 'Avenir', 'Helvetica', 'Arial', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 25px;
  margin-top: 60px;
  text-align: center;
}

button {
  background-color: #fff;
  border: 2px solid #2c3e51;
  cursor: pointer;
  font-size: 20px;
  font-weight: 600;
  outline: 0;
  padding: 10px 40px;
  position: relative;
  margin-right: 5px;
}

button:hover {
  background-color: #2c3e51;
  color: #fff;
  transition: all 0.5s;
}

@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}
</style>
