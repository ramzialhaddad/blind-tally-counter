<script lang="ts">
	import Counter from "./Counter.svelte";
	let counters: number = 0;

    function addCounter() {
        counters += 1;
	}

    function removeCounter() {
        if(counters == 0) { return}
        counters -= 1;
	}
</script>

<div class="grid grid-cols-1 gap-y-2">
	<button class="m-auto p-1 border-1 rounded" onclick={() => addCounter()}>Add Counter</button>
	<button class="m-auto p-1 border-1 rounded" onclick={() => removeCounter()}>Remove Counter</button>
</div>

<div class="grid grid-cols-2 gap-3">
	{#each Array(counters) as e}
		<Counter/>
		{e}
	{/each}
</div>