<script setup lang="ts">
import { ref } from "vue";
import FormField from "./components/FormField.vue";
import DoorForm from "./components/DoorForm.vue";
import Confetti from "./components/Confetti.vue"
import Plate from "./components/Plate.vue"

import JSConfetti from 'js-confetti'


const confetti = new JSConfetti()

  function showConfetti() {
      confetti.addConfetti({emojis: ['🧱', '🪚', '🛠', '🏗'],});
  }


const height = ref("0");
const width = ref("0");
const amount = ref(0);
const amountMass = ref(0);
const koef = 0.3335;

function calculateAmount() {
  const _width = width.value;
  const _height = height.value;

  if (!_width || !_height) {
    return;
  }

  console.log(DoorForm.data().sum)
  const k = (_width * _height) - DoorForm.data().sum / koef;
  const kg = ((_width * _height) - DoorForm.data().sum / koef) * 36;
  
  amount.value = k;
  amountMass.value = kg;

}

</script>

<template>
  <main class="mx-auto max-w-2xl py-20 px-4 md:px-0">
    <Confetti/>
    <span>
      <Plate/>
    </span>
    <h1 class="font-black text-3xl md:text-4xl mb-10">Калькулятор пазогребневых гипсовых плит</h1>

    <form @submit.prevent="calculateAmount()">
      <FormField label="Высота стены">
        <input
          required
          type="float"
          min="0,1"
          max="1000"
          v-model="height"
          class="p-1.5 px-3.5 transition-colors rounded-md border border-secondary bg-primary hover:border-accent focus:border-accent focus:outline-none shadow-md"
          placeholder="0"
        />
      </FormField>

      <FormField label="Ширина стены">
        <input
          required
          type="float"
          min="0,1"
          max="1000"
          v-model="width"
          class="p-1.5 px-3.5 transition-colors rounded-md border border-secondary bg-primary hover:border-accent focus:border-accent focus:outline-none shadow-md"
          placeholder="0"
        />
      </FormField>

      <p class="mt-10 text-5xl font-bold"> 
      <img src="./assets/perergorodka.jpeg">
      </p>
      <DoorForm/>
      <br>
      <button
        @click="showConfetti"
        type="submit"
        class="px-3.5 py-1 transition-colors rounded-md border border-secondary bg-primary enabled:hover:border-accent enabled:focus:border-accent focus:outline-none shadow-md"
      >
        Рассчитать
      </button>

      <p>
        <span class="block">ПОТРЕБУЕТСЯ ПЛИТ - {{ amount && amount.toFixed(0)}}шт</span>
      </p>
      <p>
        <span class="block">ВЕС СТЕНЫ - {{ amount && amountMass.toFixed(0)}}кг</span>
      </p>

      <p class="mt-10 text-5xl font-bold">
        <span class="block text-xl capitalize leading-10">С помощью этого простого калькулятора вы легко и просто рассчитаете:</span>
      </p>
      <p class="mt-10 text-5xl font-bold">
        <span>- </span>
        <span class="block text-xl capitalize leading-10">Количество требуемых ПГП для выкладки стены с учётом проёмов</span>
      </p>
      <p class="mt-10 text-5xl font-bold">
        <span>- </span>
        <span class="block text-xl capitalize leading-10">Общий вес стены</span>
      </p>
    </form>
  </main>

  
</template>

<style>
body {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

img {
  width: 100%;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>