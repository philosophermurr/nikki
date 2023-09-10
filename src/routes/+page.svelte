<script lang="ts">
	import { useLanyard } from 'svelte-lanyard';

	const data = useLanyard('569662811853291530');

	$: console.log($data);

	$: customStatus = $data?.activities.find((a) => a.type === 4)?.state;

	$: app = $data?.activities.find((a) => a.type !== 4)?.name;
	$: activity = $data?.activities.find((a) => a.type !== 4)?.details;
	$: details = $data?.activities.find((a) => a.type !== 4)?.state;
</script>

<body class="px-10 max-w-4xl mx-auto">
	<h1 class="mt-10">nikki &gt; you</h1>
	{#if $data}
		<div class="w-max bg-black bg-opacity-10 rounded-full pr-16">
			<table class="mt-10">
				<tr class="flex gap-7 items-center">
					<td>
						<img
							src={'https://cdn.discordapp.com/avatars/' +
								$data.discord_user.id +
								'/' +
								$data.discord_user.avatar}
							alt="my discord avatar."
							class="rounded-full h-32"
						/>
					</td>
					<td>
						<div class="flex gap-2 items-center">
							<h5>elon</h5>
							<h5 class="opacity-50 font-normal">
								{$data.discord_user.username}
							</h5>
						</div>
						<p>
							{customStatus}
						</p>
						{#if $data?.activities.find((a) => a.type === 2)}
							<div class="flex gap-2 items-center">
								<p class="font-bold">
									{app}
								</p>
								<p>&middot;</p>
								<p>
									{activity}
								</p>
								<p class="opacity-50">
									{details}
								</p>
							</div>
						{/if}
					</td>
				</tr>
			</table>
		</div>
	{:else}
		<p>Waiting to fetch Discord data...</p>
	{/if}
</body>
