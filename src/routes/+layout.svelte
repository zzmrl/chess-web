<script lang="ts">
	import '../app.css';

	let { children } = $props();
</script>

<main class="h-screen w-full bg-stone-700">
	{@render children()}
</main>

<style>
</style>
