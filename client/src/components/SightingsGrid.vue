<template lang="html">
	<div id="sightingsGrid">
		<sighting v-for="sighting in sightings" :sighting="sighting" />
	</div>
</template>

<script>
import Sighting from './Sighting';
import { eventBus } from '@/main.js'

export default {
	name: 'sightings-grid',
	components: {
		'sighting': Sighting
	},
	props: ['sightings'],
	mounted() {
		eventBus.$on('sightingDeleted', (id) => {
			this.sightings = this.sightings.filter((sighting) => {
				sighting.id !== id
			});
		});
		eventBus.$on('sightingAdded', (sighting) => {
			this.sightings.push(sighting)
		})

	}
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
