<script>
	import NavItem from '$lib/components/NavItem.svelte';
	import Home from '$lib/icons/Home.svelte';
	import Info from '$lib/icons/Info.svelte';
	import Music from '$lib/icons/Music.svelte';
	import '../app.postcss';
</script>

<div class="bg-black bg-opacity-70 backdrop-blur-md pt-10 px-10 sticky top-0 z-10">
	<!-- <div class="max-w-4xl mx-auto"> -->
		<nav class="flex">
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
			<NavItem href="/kpop">
				<div class="flex gap-2 items-center">
					<Music />
					about
				</div>
			</NavItem>
		</nav>
	<!-- </div> -->
</div>
<!-- <hr class="opacity-50" /> -->
<slot />
