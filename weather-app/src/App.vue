<template>

  <q-layout view="lHh Lpr lFf">

    <!-- Documentation q-input: https://quasar.dev/vue-components/input -->
    <q-input
        class="text-h6 border-radius-500 q-pa-md shadow-2 q-color-picker--dark"
        filled
        outlined
        rounded
        clearable
        v-model="city"
        placeholder="Ville (ex: Paris)"
        @keydown.enter.prevent="callApi"
    >
      <template v-slot:append>
        <!-- Documentation q-btn: https://quasar.dev/vue-components/button -->
        <q-btn round flat icon="fas fa-magnifying-glass" @click="callApi"
        />
      </template>
    </q-input>

    <my-temperature
        v-if="data"
        :name="data.name"
        :contry="data.sys.country"
        :value="Math.round(data.main.temp)"
        :weather="data.weather[0]">
      />
    </my-temperature>
  </q-layout>
</template>

<script>
  import myTemperature from './components/myTemperature.vue'; // Import it
export default {
  name: 'App',

  data() {
    return {
      data: null,
      apiKey: 'f6bd8d3023395506be441c8d65231e8d',
      corsProxy: 'https://cors-anywhere.herokuapp.com/',
    }
  },

  methods: {
    async callApi(newCity) {
      if (newCity !== '') {
        const request = `${this.corsProxy}api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${this.apiKey}`;
        const options = {
          method: 'GET',
          headers: {
            'Content-Type': 'application/json',
          }
        };

        this.data = await fetch(request, options)
            .then((res) => res.json())
            .then((data) => data)
            .catch((err) => {
              console.log(err);
            });
        console.log(this.data);
      }
    }
  },
  components: { // Define it
    myTemperature,
  },
}
</script>
