<template>
  <div id="app">
    <sightings-form />
    <sightings-grid :sightings="sightings" />
  </div>
</template>

<script>
import { eventBus } from '@/main.js'
import SightingsForm from './components/SightingsForm';
import SightingsGrid from './components/SightingsGrid';
import SightingService from './services/SightingService.js';
import Sighting from './components/Sighting';

export default {
  name: 'app',
  components: {
    'sightings-form': SightingsForm,
    'sightings-grid': SightingsGrid,
    'sighting': Sighting
  },
  data() {
    return {
      sightings: []
    };
  },
	mounted() {
    this.fetchSightings();

    SightingService.getSightings()
    .then(sightings => this.sightings = sightings);

    eventBus.$on('sighting-added', (sighting) => {
      this.sightings.push(sighting)
    })

    eventBus.$on('sighting-deleted', (id) => {
      let index = this.sightings.findIndex(sighting => sighting._id === id)
      this.sightings.splice(index, 1)
      // this.sightings = this.sightings.filter((sighting) => {
      //   return sighting._id != id
      }) 
    },

  methods: {
    fetchSightings() {
      SightingService.getSightings()
        .then(sightings => this.sightings = sightings);
    }
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  background: url('./assets/birds-background.jpg') no-repeat;
  height: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;

}
</style>
