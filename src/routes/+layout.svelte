<script>
	import NavItem from '$lib/components/NavItem.svelte';
	import Home from '$lib/icons/Home.svelte';
	import Info from '$lib/icons/Info.svelte';
	import '../app.postcss';
</script>

<div class="bg-black pt-10 px-10">
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
		</nav>
	<!-- </div> -->
</div>
<!-- <hr class="opacity-50" /> -->
<slot />
