<script>
	import NavItem from '$lib/components/NavItem.svelte';
	import Home from '$lib/icons/Home.svelte';
	import Info from '$lib/icons/Info.svelte';
	import Music from '$lib/icons/Music.svelte';
	import '../app.postcss';
</script>

<div class="bg-black bg-opacity-70 backdrop-blur-md pt-10 md:px-10 sticky top-0 z-10">
	<nav class="flex overflow-x-auto">
		<NavItem href="/" strict>
			<div class="flex gap-2 items-center">
				<Home />
				home
			</div>
		</NavItem>
		<NavItem href="/about">
			<div class="flex gap-2 items-center">
				<Info />
				about
			</div>
		</NavItem>
		<NavItem href="/music">
			<div class="flex gap-2 items-center">
				<Music />
				music
			</div>
		</NavItem>
	</nav>
</div>

<main class="max-w-4xl mx-auto my-10 px-8">
	<slot />
</main>