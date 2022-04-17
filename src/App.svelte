<script lang="ts">
	import Dihotomiya from "./Dihotomiya.svelte";
	import Gold from "./Gold.svelte";
	import Swann from "./Swann.svelte";
	import Fibonacci from "./Fibonacci.svelte";
	const methods: object[] = [
		{
			"id": "One",
			"component": Swann,
			"name": "Метод Свена",
			"passed": false
		},
		{
			"id": "Two",
			"component": Dihotomiya,
			"name": "Метод дихотомии",
			"passed": true
		},
		{
			"id": "Three",
			"component": Fibonacci,
			"name": "Метод Фибоначчи",
			"passed": false
		},
		{
			"id": "Four",
			"component": Gold,
			"name": "Метод золотого сечения",
			"passed": true
		},
	]
</script>

<main>
	<h1>Методы оптимизации!</h1>
	<div class="accordion" id="accordionExample">
		{#each methods as method(method.id)}
			<div class="accordion-item">
				<h2 class="accordion-header" id="heading{method.id}">
					{#if method.passed}
						<button class="accordion-button bg-success text-light" type="button" data-bs-toggle="collapse" data-bs-target="#collapse{method.id}" aria-expanded="true" aria-controls="collapse{method.id}">
							{method.name}
						</button>
					{:else}
						<button class="accordion-button bg-danger text-light" type="button" data-bs-toggle="collapse" data-bs-target="#collapse{method.id}" aria-expanded="true" aria-controls="collapse{method.id}">
							{method.name}
						</button>
					{/if}
				</h2>
				<div id="collapse{method.id}" class="accordion-collapse collapse show" aria-labelledby="heading{method.id}" data-bs-parent="#accordionExample">
					<div class="accordion-body">
						<svelte:component this={method.component}/>
					</div>
				</div>
			</div>
		{/each}
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>