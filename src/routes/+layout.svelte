<script>
	import NavItem from '$lib/components/NavItem.svelte';
	import '../app.postcss';
</script>

<nav class="flex">
	<NavItem href="/" strict>home</NavItem>
	<NavItem href="/about">about</NavItem>
</nav>
<hr />
<slot />
