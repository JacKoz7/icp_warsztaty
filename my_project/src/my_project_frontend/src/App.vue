<script lang="ts">
import { ref } from 'vue';
// import { my_project_backend } from 'declarations/my_project_backend/index';

export default {
  data(){
    return{
      kursy: []
    }
  },
  methods: {
    async getexchangerates(){
      const url = `${window.location.origin}/api/exchangerates/tables/a/?format=json`;
      const response = await fetch(url);

      const responsJson = await response.json();
      this.kursy = responsJson[0].rates;

    }
  },
  async mounted() { // uruchamian rzeczy w momenencie montowania strony
    await this.getexchangerates();
  }
}


</script>
<template>
  <main class="container mx-auto p-4">
    <table class="w-full border-collapse table-auto">
      <thead class="bg-lime-500 text-white">
        <tr>
          <th scope="col" class="px-6 py-3 text-left">Waluta</th>
          <th scope="col" class="px-6 py-3 text-left">Kod</th>
          <th scope="col" class="px-6 py-3 text-left">Cena</th>
        </tr>
      </thead>
      <tbody class="bg-white divide-y divide-gray-200">
        <tr v-for="kurs in kursy" class="hover:bg-gray-50">
          <th scope="row" class="px-6 py-4 text-left">{{ kurs.currency }}</th>
          <td class="px-6 py-4">{{ kurs.code }}</td>
          <td class="px-6 py-4">{{ kurs.mid }}</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
