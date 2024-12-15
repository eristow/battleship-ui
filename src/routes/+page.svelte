<script lang="ts">
	/*
	export interface ShipSummary {
		name: ShipType;
		length: number;
		startX?: number;
		startY?: number;
		isHorizontal?: boolean;
		currentHits?: number;
	}
	*/
	let backend_url = import.meta.env.VITE_BACKEND_URL;
	let ships = fetchShipTypes();

	async function fetchShipTypes() {
		const response = await fetch(`${backend_url}/games/ships`);
		return await response.json();
	}
</script>

<div class="m-2">
	{#await ships}
		<p>Loading...</p>
	{:then response}
		{#each response as ship}
			<p>{ship.name}: length of {ship.length}</p>
		{/each}
	{:catch error}
		<p>{error}</p>
	{/await}
</div>
