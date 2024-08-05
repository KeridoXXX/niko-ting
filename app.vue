<template>
  <div class="container mx-auto p-4">
    <div class="flex justify-center mb-8">
      <div class="w-full max-w-2xl flex flex-col items-center relative">
        <h1 class="font-serif text-[4rem] absolute top-4">Niko's</h1>
        <img src="assets/img/aHR0cHM6Ly93d3cubGFnZXJzYWxnLmNvbS9zdG9yYWdlL2ltYWdlcy9zYWxlcy9haWF5dS9sb2dvLWJsYWNrLnBuZw==.png" alt="" class="mt-16 mb-4">
        <h1 class="font-serif text-[4rem] absolute bottom-4">Udregner</h1>
      </div>
    </div>

    <!-- Month Selector -->
    <div class="mb-8 text-center">
      <h1 class="text-xl font-semibold mb-4">Vælg måned for udregning</h1>
      <form>
        <select name="date-selector" id="date-selector" v-model="selectedMonth" class="p-2 border border-gray-300 rounded">
          <option v-for="month in monthData" :value="month" :key="month.name">{{ month.name }}</option>
        </select>
      </form>
    </div>

    <div>
      <form class="flex flex-col items-center gap-4" @submit.prevent="calculateTotals">
        <div class="flex flex-col mb-4" v-for="day in selectedMonth.dage" :key="day">
          <span class="font-medium">{{ day }}. {{ selectedMonth.name }}</span>
          <div class="flex gap-2">
            <div>
              <p>Fortjeneste:</p>
              <input
              type="number"
              :name="'fortjeneste' + day"
              placeholder="Indtast fortjeneste"
              v-model.number="fortjeneste[day - 1]"
              class="p-2 border border-gray-300 rounded flex-1"
            />
            </div>

            <div>
              <div>Ekspiditioner:</div>
              <input
              type="number"
              :name="'ekspiditioner' + day"
              placeholder="Indtast ekspiditioner"
              v-model.number="ekspiditioner[day - 1]"
              class="p-2 border border-gray-300 rounded flex-1"
            />
            </div>

          </div>
        </div>
        <button type="submit" class="self-center bg-blue-500 text-white p-2 rounded">Foretag Aiayu-udregning</button>
      </form>
    </div>

    <div v-if="totalFortjeneste !== null && totalEkspiditioner !== null" class="mt-8 text-center">
      <h2 class="text-2xl font-semibold">Total Fortjeneste: {{ totalFortjeneste }}</h2>
      <h2 class="text-2xl font-semibold">Totale Ekspiditioner: {{ totalEkspiditioner }}</h2>
    </div>
  </div>
</template>


<script setup>

const monthData = [{name: 'januar', dage: 31}, {name: 'februar', dage: 28}, {name: 'marts', dage: 31}, {name: 'april', dage: 30}, {name: 'maj', dage: 31}, {name: 'juni', dage: 30}, {name: 'juli', dage: 31}, {name: 'august', dage: 31}, {name: 'september', dage: 30}, {name: 'oktober', dage: 31}, {name: 'november', dage: 30}, {name: 'december', dage: 31}]

const selectedMonth = ref(monthData[0]);
const fortjeneste = reactive(Array(31).fill(0));
const ekspiditioner = reactive(Array(31).fill(0));
const totalFortjeneste = ref(null);
const totalEkspiditioner = ref(null);

watch(selectedMonth, () => {
  fortjeneste.fill(0);
  ekspiditioner.fill(0);
  totalFortjeneste.value = null;
  totalEkspiditioner.value = null;
});

const calculateTotals = () => {
  totalFortjeneste.value = fortjeneste.reduce((acc, value) => acc + (value || 0), 0);
  totalEkspiditioner.value = ekspiditioner.reduce((acc, value) => acc + (value || 0), 0);
};

// omsætning for butikken hver måned
// 31 dages omsætning
// total sum af mængden af dages fortjeneste

// total fortjeneste
// totale ekspiditioner

// month selector
// fortjeneste input 
// ekspiditions input


</script>

