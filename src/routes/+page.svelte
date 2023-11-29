<script lang="ts">
	import { useLanyard } from 'sk-lanyard';

	const data = useLanyard({ method: 'ws', id: '569662811853291530' });

	$: customStatus = $data?.activities.find((a) => a.type === 4);

	$: activityStatus = $data?.activities.find((a) => a.type !== 4);
	$: app = $data?.activities.find((a) => a.type !== 4)?.name?.toLowerCase();
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

<h1>nikki &gt; you</h1>
<p class="mt-4">&lsqb;insert text here eventually&rsqb;</p>
<div class="bg-zinc-900 flex rounded-full pr-8 mt-6">
	{#if $data}
		<div class="flex items-center gap-5">
			<div class="relative shrink-0">
				<img
					src={'https://cdn.discordapp.com/avatars/' +
						$data.discord_user.id +
						'/' +
						$data.discord_user.avatar}
					alt=""
					class="rounded-full w-20 h-20 md:h-32 md:w-32 bg-zinc-800"
				/>
				<div
					class={`absolute bottom-1 right-1 w-4 h-4 md:w-6 md:h-6 rounded-full ring-[6px] md:ring-6 ring-zinc-900 ${getStatusColor(
						$data.discord_status
					)} group flex justify-center`}
				/>
			</div>
			<div>
				<div class="line-clamp-1 break-all text-lg text-zinc-500">
					{#if $data.discord_user.display_name}
						<span class="font-bold text-white title">
							{$data.discord_user.display_name}
						</span>
						<span class="italic">
							{$data.discord_user.username}
						</span>
					{:else}
						<span class="font-bold">
							{$data.discord_user.username}
						</span>
					{/if}
				</div>
				<div class="flex gap-2 items-center">
					{#if customStatus}
						{@const { emoji } = customStatus}

						{#if emoji?.id}
							<img
								src={'https://cdn.discordapp.com/emojis/' + emoji.id}
								alt=""
								title={':' + emoji.name +':'}
								class="h-5 cursor-pointer"
							/>
						{:else if emoji?.name}
							{emoji.name}
						{/if}
						{#if customStatus.state}
							<span class="line-clamp-1 break-all">
								{customStatus.state}
							</span>
						{/if}
					{/if}
				</div>
				{#if activityStatus}
					<div class="flex gap-2 items-center">
						<p class="font-bold title text-base">
							<span class="line-clamp-1 break-all max-w-xs">
								{app}
							</span>
						</p>
						{#if activity}
							<p>&middot;</p>
							<p>
								<span class="line-clamp-1 break-all max-w-sm">
									{activity}
								</span>
							</p>
						{/if}
						<p class="text-zinc-500">
							{#if details}
								<span class="line-clamp-1 break-all max-w-xs italic">
									{details}
								</span>
							{/if}
						</p>
					</div>
				{/if}
			</div>
		</div>
	{:else}
		<div class="h-32 w-32 rounded-full bg-zinc-800" />
	{/if}
</div>
