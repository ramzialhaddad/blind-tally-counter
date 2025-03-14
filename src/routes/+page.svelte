<script lang="ts">
	import Counter from "./Counter.svelte";
	let counters: number = 0;
    let showValuesFlag:boolean = false;

    function addCounter() {
        counters += 1;
	}

    function removeCounter() {
        if(counters == 0) { return}
        counters -= 1;
	}

    function showValues(){
        showValuesFlag = !showValuesFlag;
	}
</script>

<div class="flex justify-center gap-4 p-2">
	<button class="p-1 border-1 rounded text-white" onclick={() => addCounter()}>Add Counter</button>
	<button class="p-1 border-1 rounded text-white" onclick={() => removeCounter()}>Remove Counter</button>
	<button class="p-1 border-1 rounded text-white" onclick={() => showValues()}>Show values</button>
</div>

<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-3 p-2">
	{#each Array(counters) as e}
		<Counter showValues={showValuesFlag}/>
		{e}
	{/each}
</div>