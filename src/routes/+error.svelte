<script>
	import { page } from '$app/stores';
</script>

<body class="px-10 max-w-4xl mx-auto">
	<h1 class="mt-10">error {$page.status}: {$page.error?.message.toLowerCase()}</h1>
</body>
