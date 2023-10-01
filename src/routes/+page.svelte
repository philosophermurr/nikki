<script lang="ts">
	import { useLanyard } from 'sk-lanyard';

	const data = useLanyard({ method: 'ws', id: '569662811853291530' });

	$: customStatus = $data?.activities.find((a) => a.type === 4);
	$: emoji = $data?.activities.find((a) => a.type === 4)?.emoji?.id;
	$: emojiName = $data?.activities.find((a) => a.type === 4)?.emoji?.name;
	$: text = $data?.activities.find((a) => a.type === 4)?.state;

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
<div class="bg-zinc-900 flex rounded-full pr-16 mt-6">
	{#if $data}
		<div class="flex items-center gap-5">
			<div class="relative">
				<img
					src={'https://cdn.discordapp.com/avatars/' +
						$data.discord_user.id +
						'/' +
						$data.discord_user.avatar}
					alt=""
					class="rounded-full h-32 w-32 bg-zinc-800 shrink-0"
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
					{#if customStatus}
						{#if emoji}
							<img
								src={'https://cdn.discordapp.com/emojis/' + emoji}
								alt=""
								title={':' + emojiName + ':'}
								class="h-5 cursor-pointer"
							/>
						{/if}
						<span class="line-clamp-1 break-all">
							{text}
						</span>
					{/if}
				</div>
				{#if activityStatus}
					<div class="flex gap-2 items-center">
						<p class="font-bold">
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
						<p class="opacity-50">
							{#if details}
								<span class="line-clamp-1 break-all max-w-xs">
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
