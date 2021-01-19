<template lang="html">
	<div id="sightingsGrid">
		<sighting v-for="(sighting, index) in sightings" :key="index" :sighting="sighting" />
	</div>
</template>

<script>

import { eventBus } from '@/main.js'
import SightingService from '@/services/SightingService.js'
import Sighting from './Sighting';

export default {
	name: 'sightings-grid',
	components: {
		'sighting': Sighting
	},
  props: ['sightings']
  
}
</script>

<style lang="css" scoped>
#sightingsGrid {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-evenly;
}

h2 {
	padding: 0;
	margin: 0;
}
</style>
