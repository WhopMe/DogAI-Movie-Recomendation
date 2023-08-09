<script>
	import LoadingIndicator from './Loading.svelte';

	/**
	 * @type string
	 */
	export let cinemaType;
	/**
	 * @type Array<string>
	 */
	export let selectedCategories;
	/**
	 * @type string
	 */
	export let specificDescriptors;
	/**
	 * @type Boolean
	 */
	export let loading;

	const categoryTypes = [
		'动作',
		'冒险',
		'动画',
		'传记',
		'喜剧',
		'犯罪',
		'纪录片',
		'剧情',
		'家庭',
		'奇幻',
		'黑色电影',
		'历史',
		'恐怖',
		'音乐',
		'悬疑',
		'浪漫',
		'科幻',
		'体育',
		'惊悚',
		'战争',
		'西部',
		'艺术片',
		'黑色喜剧',
		'流行影片',
		'黑帮电影',
		'黑色幽默',
		'史诗',
		'情色',
		'实验',
		'童话',
		'影片中的影片',
		'未来',
		'帮派',
		'抢劫',
		'历史题材',
		'假日',
		'独立制作',
		'青少年',
		'悲剧',
		'怪物',
		'政治',
		'心理',
		'公路电影',
		'讽刺',
		'科幻',
		'闹剧',
		'社会问题',
		'超级英雄',
		'超现实',
		'青少年',
		'吸血鬼',
		'僵尸'
	];

	let cinemaTypes = [
		{ value: '电视剧', title: '电视剧' },
		{ value: '电影', title: '电影' },
		{ value: '电视剧或电影', title: '无偏好' }
	];
</script>

<div class="pt-6 md:pt-10 text-slate-200">
	<div>
		<div class="mb-8">
			<div class="mb-4 font-semibold text-lg">你在寻找什么类型的影视作品？</div>
			<div class="flex items-center">
				{#each cinemaTypes as type (type.value)}
					<button
						on:click={() => {
							cinemaType = type.value;
						}}
						class={`${
							cinemaType === type.value ? 'bg-pink-600/40' : ''
						} text-slate-200 font-bold mr-2 text-sm mt-2 py-2 px-4 rounded-full border border-pink-600`}
					>
						{type.title}
					</button>
				{/each}
			</div>
		</div>
		<div>
			<div class="mb-4 font-semibold text-lg">
				请选择您希望影视作品包含的所有类别。
			</div>
			<div class="flex items-center flex-wrap">
				{#each categoryTypes as category}
					<label
						class={`${
							selectedCategories.includes(category) ? 'bg-pink-600/40' : ''
						} text-slate-200 font-bold mr-2 mt-2 text-sm py-2 px-4 rounded-full border border-pink-600`}
					>
						<input
							class="hidden"
							type="checkbox"
							bind:group={selectedCategories}
							name="categories"
							value={category}
						/>
						{category}
					</label>
				{/each}
			</div>
		</div>
		<div class="mt-8">
			<div class="mb-4 font-semibold text-lg">
				在此处写下任何其他规格要求。尽量详细地描述。
			</div>
			<textarea
				bind:value={specificDescriptors}
				class="bg-white/40 border border-white/0 p-2 rounded-md placeholder:text-slate-800 text-slate-900 w-full h-20 font-medium"
				placeholder="例如：必须至少有2个季节，可在 Netflix 或 Hulu 上观看。"
			/>
			<button
				on:click
				class={`${
					loading
						? 'bg-pink-400/50'
						: 'bg-pink-600 hover:bg-gradient-to-r from-pink-700 via-pink-600 to-pink-700 '
				} mt-4 w-full h-10 text-white font-bold p-3 rounded-full flex items-center justify-center`}
			>
				{#if loading}
					<LoadingIndicator />
				{:else}
					<p>精选我的列表</p>
				{/if}
			</button>
		</div>
	</div>
</div>
