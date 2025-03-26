<script lang="ts">
	const board =
		'♖♘♗♔♕♗♘♖' +
		'♙♙♙♙♙♙♙♙' +
		'        ' +
		'        ' +
		'        ' +
		'        ' +
		'♟♟♟♟♟♟♟♟' +
		'♜♞♝♚♛♝♞♜';
</script>

<div class="board">
	{#each { length: 8 }, row}
		{#each { length: 8 }, col}
			<div class:dark={(row + col) % 2 === 0}></div>
		{/each}
	{/each}
</div>

<style>
	.board {
		display: grid;
		aspect-ratio: 1;
		grid-template-columns: repeat(8, minmax(0, 1fr));
		border: 1px solid;
		background: var(--color-bg, gray);
		gap: 0.25rem;
		width: 100%;

		* {
			background: var(--color-light, white);
		}

		.dark {
			background: var(--color-dark, black);
		}
	}
</style>
