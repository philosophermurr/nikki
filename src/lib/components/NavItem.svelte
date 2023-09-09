<script lang="ts">
	import { page } from '$app/stores';

	export let href: string;
	export let strict = false;

	$: active = strict ? $page.url.pathname === href : $page.url.pathname.startsWith(href);
</script>

<div class="flex ml-2 md:ml-0 border-b-2 {active ? 'border-b-rose-500' : 'border-b-transparent'}">
	<a class="btn" {href}>
		<div class="flex items-center gap-2 {active ? 'font-bold' : 'font-normal text-gray-700'}">
			<slot />
		</div>
	</a>
</div>