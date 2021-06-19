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
body {
  background-color: #b8deeb;
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
</style>
