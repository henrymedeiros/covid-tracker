<template>
    <main v-if="!loading">
      <DataTitle :title="title" :dataDate="dataDate"/>
      <DataBoxes :stats="stats"/>
      <CountrySelect @get-country="getCountryData" :countries="countries"/>
      <button @click='clearCountryData' v-if='stats.Country' class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">
        Clear Country
      </button>
    </main>
    <main v-else class='flex flex-col items-center justify-center text-center '>
      <div class="text-gray-500 text-2xl mt-10 mb-6">
        Fetching Data...
      </div>
      <img src="@/assets/loading.gif" alt="loading" class='loading-image'>
      
      
    </main>

</template>

<style scoped>
.loading-image{
  width: 64px;
}
</style>

<script>
// @ is an alias to /src
import api from "../services/api.js";
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import CountrySelect from "../components/CountrySelect.vue";

export default {
    name: "Home",
    components: {
      DataTitle, DataBoxes, CountrySelect
    },
    data() {
        return {
            loading: true,
            title: 'Global',
            stats: null,
            dataDate: "",
            countries: []

        };
    },
    methods: {
        async fetchCovidData(endpoint) {
            const response = await api.get(endpoint);
            return response.data;
        },
        getCountryData(country){
          this.stats = country
          this.title = country.Country
        },
        async clearCountryData(){
          this.loading = true
          const data = await this.fetchCovidData('/summary')
          this.title = 'Global'
          this.stats = data.Global
          this.loading = false
        }
    },
    async created() {
        const data = await this.fetchCovidData("/summary");
        console.log(data);

        this.dataDate = data.Date;
        this.loading = false
        this.stats = data.Global
        this.countries = data.Countries;
    },
};
</script>
