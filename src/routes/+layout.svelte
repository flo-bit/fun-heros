<script>
	import '../app.css';

	import ThemeToggle from '$lib/components/ThemeToggle.svelte';
</script>

<slot />

<div class="fixed top-4 right-4">
	<ThemeToggle />
</div>
