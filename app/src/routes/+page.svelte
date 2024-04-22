<svelte:head>
	<title>Piškvorky</title>
	<meta name="description" content="Piškvorky demo app" />
</svelte:head>

<section>
	<h1>Piškvorky</h1>
	<div id="board">
		{#each Array(3).fill() as _, row}
			<div class="row">
				{#each Array(3).fill() as _, col}
					<div class="cell"></div>
				{/each}
			</div>
		{/each}
	</div>
</section>
