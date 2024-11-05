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
      const url = `$(window.location.origin)/api/exchangerates/tables/a/?format=json`;
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
  <main class="container mx-auto">
    <table class='w-full'>
      <thead class="lime-500">
        <tr>
          <th scope="col">Waluta</th>
          <th scope="col">Kod</th>
          <th scope="col">Cena</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="kurs in kursy">
          <th scope="row">{{ kurs.currency }}</th>
          <td>{{ kurs.code }}</td>
          <td>{{ kurs.mid }}</td>
        </tr>
      </tbody>
    </table>
  </main>
</template>
