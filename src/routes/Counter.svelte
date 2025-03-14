<script lang="ts">
	let {showValues} = $props();

	let positive = $state(0);
    let negative = $state(0);
    let name = $state("Untitled");
	let colour = $state('white');
	let colours = ['red', 'blue', 'orange', 'green', 'yellow', 'white'];
	let editing: boolean = $state(false);

    // Convert this to explicit type so typescript isnt angry in line 231
    let borderColour = {'white':'border-white',
						'red':'border-red-500',
        				'blue':'border-blue-500',
						'orange':'border-orange-500',
						'green':'border-green-500',
						'yellow':'border-yellow-500',};

    function addPositive(){
        positive++;
	}

    function addNegative(){
        negative++;
	}

    function edit(){
        editing = !editing;
	}
</script>

<style>
	.button-red-pushable {
		  position: relative;
		  border: none;
		  background: transparent;
		  padding: 0;
		  cursor: pointer;
		  outline-offset: 4px;
		  transition: filter 250ms;
		  user-select: none;
		  -webkit-user-select: none;
		  touch-action: manipulation;
	  }

	.button-red-shadow {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		border-radius: 12px;
		background: hsl(0deg 0% 0% / 0.25);
		will-change: transform;
		transform: translateY(2px);
		transition:
			transform
			600ms
			cubic-bezier(.3, .7, .4, 1);
	}

	.button-red-edge {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		border-radius: 12px;
		background: hsl(340deg 100% 32%);
	}

	.button-red-front {
        display: flex;
        align-items: center;
        justify-content: center;
		position: relative;
		padding: 12px 27px;
		border-radius: 12px;
		font-size: 1.1rem;
		color: white;
		background: hsl(345deg 100% 47%);
		will-change: transform;
		transform: translateY(-4px);
		transition:
			transform
			600ms
			cubic-bezier(.3, .7, .4, 1);
	}

	@media (min-width: 768px) {
		.button-red-front {
			font-size: 1.25rem;
			padding: 12px 42px;
		}
	}

	.button-red-pushable:hover {
		filter: brightness(110%);
		-webkit-filter: brightness(110%);
	}

	.button-red-pushable:hover .button-red-front {
		transform: translateY(-6px);
		transition:
			transform
			250ms
			cubic-bezier(.3, .7, .4, 1.5);
	}

	.button-red-pushable:active .button-red-front {
		transform: translateY(-2px);
		transition: transform 34ms;
	}

	.button-red-pushable:hover .button-red-shadow {
		transform: translateY(4px);
		transition:
				transform
				250ms
				cubic-bezier(.3, .7, .4, 1.5);
	}

	.button-red-pushable:active .button-red-shadow {
		transform: translateY(1px);
		transition: transform 34ms;
	}

	.button-red-pushable:focus:not(:focus-visible) {
		outline: none;
	}

	/*Green Button*/
    .button-green-pushable {
        position: relative;
        border: none;
        background: transparent;
        padding: 0;
        cursor: pointer;
        outline-offset: 4px;
        transition: filter 250ms;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
    }

    .button-green-shadow {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border-radius: 12px;
        background: hsl(0deg 0% 0% / 0.25);
        will-change: transform;
        transform: translateY(2px);
        transition:
                transform
                600ms
                cubic-bezier(.3, .7, .4, 1);
    }

    .button-green-edge {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border-radius: 12px;
		background: green;
    }

    .button-green-front {
    	display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
		padding: 12px 27px;
		border-radius: 12px;
		font-size: 1.1rem;
		color: white;
		background: hsl(80, 100%, 34%);
		will-change: transform;
		transform: translateY(-4px);
		transition: transform 600ms cubic-bezier(.3, .7, .4, 1);
		cursor: pointer;
    }

    @media (min-width: 768px) {
        .button-green-front {
            font-size: 1.25rem;
            padding: 12px 42px;
        }
    }

    .button-green-pushable:hover {
        filter: brightness(110%);
        -webkit-filter: brightness(110%);
    }

    .button-green-pushable:hover .button-green-front {
        transform: translateY(-6px);
        transition:
                transform
                250ms
                cubic-bezier(.3, .7, .4, 1.5);
    }

    .button-green-pushable:active .button-green-front {
        transform: translateY(-2px);
        transition: transform 34ms;
    }

    .button-green-pushable:hover .button-green-shadow {
        transform: translateY(4px);
        transition:
                transform
                250ms
                cubic-bezier(.3, .7, .4, 1.5);
    }

    .button-green-pushable:active .button-green-shadow {
        transform: translateY(1px);
        transition: transform 34ms;
    }

    .button-green-pushable:focus:not(:focus-visible) {
        outline: none;
    }
</style>

<div class="border-2 {borderColour[colour]} rounded-2xl p-4 grid grid-cols-1 gap-y-10 relative">
	{#if !showValues}
		<div class="flex justify-between items-center max-w-auto">
			{#if editing}
				<div class="flex flex-col gap-1 max-w-3/4">
					<input style="color: {colour};" type="text" bind:value={name} class="border-1 text-3xl font-semibold">
					<div class="flex gap-1 justify-between">
						{#each colours as c}
							<button
								class="aspect-square rounded-[50%]"
								style="background: {c}; aspect-ratio:1; padding:0.5rem 1rem;"
								aria-label={c}
								onclick={() => colour = c}
							></button>
						{/each}
					</div>
				</div>
			{:else}
				<h1 style="color: {colour};" class="text-3xl font-semibold">{name}</h1>
			{/if}
			<button onclick={()=>edit()} class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full cursor-pointer">
				{#if editing}
					Save
				{:else}
					Edit Name
				{/if}

			</button>
		</div>

	<!--	<button class="m-auto p-1 border-1 rounded bg-green-400" onclick={() => addPositive()}>Add Positive</button>-->
	<!--	<button class="m-auto p-1 border-1 rounded bg-red-600" onclick={() => addNegative()}>Add Negative</button>-->

		<!-- https://getcssscan.com/css-buttons-examples "Button 82" by Josh W Comeau-->
		<button class="button-green-pushable" onclick={()=>addPositive()}>
			<span class="button-green-shadow"></span>
			<span class="button-green-edge"></span>
			<span class="button-green-front text h-30">
				Add Positive
			</span>
		</button>
		<button class="button-red-pushable" onclick={()=> addNegative()}>
			<span class="button-red-shadow"></span>
			<span class="button-red-edge"></span>
			<span class="button-red-front text h-30">
				Add Negative
			</span>
		</button>

		<!-- WIP tailwind conversion
		<button class="relative border-none bg-transparent p-0 cursor-pointer outline-offset-4 transition-filter duration-250
		 select-none touch-manipulation group">
			<!- Shadow
			<span class="absolute top-0 left-0 w-full h-full rounded-lg bg-black/25 will-change-transform transform
			translate-y-2 duration-100 transition-[cubic-bezier(.3,.7,.4,1)] group-hover:translate-y-3
			group-active:translate-y-1"></span>

			<!- Side of button
			<span class="absolute top-0 left-0 w-full h-full rounded-lg bg-gradient-to-l from-[#550000] to-[#550000]/80">
			</span>

			<!- Rest of button
			<span class="block relative py-3 px-6 rounded-lg text-white bg-[#FF2B2B] will-change-transform
			 -translate-y-1 transition-transform duration-100 transform-[cubic-bezier(.3,.7,.4,1)]
			 group-hover:-translate-y-2 group-active:-translate-y-1">
				Test
			</span>
		</button> -->
	{:else}
		<div>
			<h1 style="color: {colour};" class="text-3xl font-semibold">{name}</h1>
			<p class="text-white">Positive: {positive}</p>
			<p class="text-white">Negative: {negative}</p>
			<p class="{(positive-negative) >= 0 ? positive-negative > 0 ? 'text-green-500' : 'text-white' : 'text-red-500'}">Difference: {positive - negative}</p>
		</div>
	{/if}
</div>