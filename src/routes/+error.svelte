<script>
	import { page } from '$app/stores';
</script>

<body class="max-w-4xl mx-auto">
	<h1 class="mt-10">{$page.status}: {$page.error?.message.toLowerCase()}</h1>
	<p class="mt-4">
		try going back <a
			href="/"
			class="text-rose-500 hover:text-rose-400 hover:font-bold transition-all">home</a
		>?
	</p>
</body>
