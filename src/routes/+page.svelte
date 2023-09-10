<script lang="ts">
	import { useLanyard } from 'sk-lanyard';

	const data = useLanyard({ method: 'rest', id: '569662811853291530' });

	$: console.log($data);

	$: emoji = $data?.activities.find((a) => a.type === 4)?.emoji?.id;
	$: customStatus = $data?.activities.find((a) => a.type === 4)?.state;

	$: app = $data?.activities.find((a) => a.type !== 4)?.name.toLowerCase();
	$: activity = $data?.activities.find((a) => a.type !== 4)?.details?.toLowerCase();
	$: details = $data?.activities.find((a) => a.type !== 4)?.state?.toLowerCase();

	const statusColors: Record<string, string> = {
		online: 'bg-emerald-500',
		idle: 'bg-amber-400',
		dnd: 'bg-rose-400'
	};

	const getStatusColor = (status: string) => {
		if (!status) return 'bg-gray-400';

		const str = statusColors[status];

		if (!str) return 'bg-gray-400';

		return str;
	};
</script>

<body class="px-10 max-w-4xl mx-auto">
	<h1 class="mt-10">nikki &gt; you</h1>
	{#if $data}
		<div class="bg-zinc-900 flex rounded-full pr-16 mt-10">
			<div class="flex items-center gap-5">
				<div class="relative">
					<img
						src={'https://cdn.discordapp.com/avatars/' +
							$data.discord_user.id +
							'/' +
							$data.discord_user.avatar}
						alt="my discord avatar"
						class="rounded-full h-32"
					/>
					<div
						class={`absolute top-24 right-1 w-4 h-4 md:w-6 md:h-6 rounded-full ring-[6px] md:ring-6 ring-zinc-900 ${getStatusColor(
							$data.discord_status
						)} group flex justify-center`}
					/>
				</div>
				<div>
					<div class="flex gap-2 items-center">
						{#if $data.discord_user.display_name}
							<h5>
								{$data.discord_user.display_name}
							</h5>
							<h5 class="opacity-50 font-normal">
								{$data.discord_user.username}
							</h5>
						{:else}
							<h5>
								{$data.discord_user.username}
							</h5>
						{/if}
					</div>
					<div class="flex gap-2 items-center">
						{#if $data?.activities.find((a) => a.type === 4)}
							{#if emoji}
								<img
									src={'https://cdn.discordapp.com/emojis/' + emoji}
									alt="the custom emoji in my status"
									class="h-5"
								/>
							{/if}
							<span class="line-clamp-1 break-all">
								{customStatus}
							</span>
						{/if}
					</div>
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
								{#if details}
									{details}
								{/if}
							</p>
						</div>
					{/if}
				</div>
			</div>
		</div>
	{:else}
		<p class="mt-10">Waiting to fetch Discord data...</p>
	{/if}
</body>
