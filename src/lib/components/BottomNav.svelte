<script lang="ts">
	import { page } from '$app/state';

	interface MoreItem {
		title: string;
		href?: string;
		badge?: string;
		isSoon?: boolean;
		isExternal?: boolean;
	}

	let activeSheet = $state<string | null>(null);

	function toggleSheet(id: string) {
		activeSheet = activeSheet === id ? null : id;
	}

	function closeSheet() {
		activeSheet = null;
	}

	const appsItems = [
		{
			title: 'E-Budget',
			desc: 'Budgeting & expenditure tracking',
			href: 'https://e-budget.masagung.my.id',
			isExternal: true,
			badge: 'v1'
		}
	];

	const purwaItems = [
		{
			title: 'Portal Web',
			desc: 'Web Portal Purwatech Solutions',
			href: 'https://portal.purwatechsolutions.com',
			isExternal: true,
			badge: 'V1'
		},
		{
			title: 'Business Management System',
			desc: 'Business Management System App',
			href: 'https://bms.purwatechsolutions.com',
			isExternal: true,
			badge: 'V1'
		}
	];

	const projectItems = [
		{
			title: 'Purwa Digital',
			desc: 'Platform ekosistem & layanan digital',
			children: [
				{ title: 'Admin', desc: 'Dashboard & kontrol manajemen', href: 'https://admin.purwa-digital.purwatechsolutions.com', isExternal: true, badge: 'Admin' },
				{ title: 'Guest', desc: 'Portal publik & pengunjung', href: 'https://purwa-digital.purwatechsolutions.com/', isExternal: true, badge: 'Live' }
			]
		},
		{ title: 'Purwa Bengkel', desc: 'Sistem operasional & manajemen bengkel', badge: 'Soon', isSoon: true },
		{ title: 'Purwa Mabar', desc: 'Komunitas & platform event gaming', badge: 'Soon', isSoon: true }
	];

	const moreItems: { label: string; items: MoreItem[] }[] = [
		{ label: 'Growth', items: [
			{ title: 'Work & Career English', href: '/growth/english', badge: 'Active' },
			{ title: 'General & Daily English', href: '/growth/english/general', badge: 'Active' },
			{ title: 'IOT', badge: 'Soon', isSoon: true }
		]},
		{ label: 'Technologies', items: [
			{ title: '.NET Core', badge: 'Soon', isSoon: true },
			{ title: 'NestJS', badge: 'Soon', isSoon: true },
			{ title: 'React.js & Svelte', badge: 'Soon', isSoon: true },
			{ title: 'Logging & Tracing', badge: 'Soon', isSoon: true },
			{ title: 'Security & Auth', badge: 'Soon', isSoon: true },
			{ title: 'Database & Caching', badge: 'Soon', isSoon: true },
			{ title: 'Message Broker', badge: 'Soon', isSoon: true }
		]},
		{ label: 'Challenges', items: [
			{ title: '.NET Mid → Advanced', href: '/challenges/dotnet', badge: 'Active' },
			{ title: 'K6 Load Testing', href: '/challenges/k6', badge: 'Active' },
			{ title: 'Kubernetes & DevOps', href: '/challenges/kubernetes', badge: 'Active' },
			{ title: 'MySQL Advanced', href: '/challenges/mysql', badge: 'Active' },
			{ title: 'SQL Server Advanced', href: '/challenges/sqlserver', badge: 'Active' }
		]},
		{ label: 'Links', items: [
			{ title: 'Jira Software', href: 'https://agungkusaeri.atlassian.net/jira/for-you?tab=workedon', isExternal: true },
			{ title: 'GitHub Profile', href: 'https://github.com/agungkusaeri9', isExternal: true }
		]}
	];

	const currentPath = $derived(page.url.pathname);
</script>

<svelte:window onclick={() => activeSheet = null} />

{#if activeSheet}
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<div
		class="fixed inset-0 bg-black/30 backdrop-blur-sm z-[90] lg:hidden"
		onclick={closeSheet}
		onkeydown={(e) => { if (e.key === 'Escape') closeSheet(); }}
	></div>
{/if}

{#if activeSheet}
	<!-- svelte-ignore a11y_no_static_element_interactions -->
	<div
		class="fixed bottom-16 left-0 right-0 z-[95] lg:hidden"
		onclick={(e) => e.stopPropagation()}
		onkeydown={(e) => { if (e.key === 'Escape') closeSheet(); }}
	>
		<div class="mx-2 mb-1 bg-white rounded-2xl border border-slate-200 shadow-2xl max-h-[60vh] overflow-y-auto">
			<div class="sticky top-0 bg-white/95 backdrop-blur-sm border-b border-slate-100 px-4 py-3 flex items-center justify-between rounded-t-2xl">
				<span class="text-sm font-bold text-slate-800">
					{activeSheet === 'apps' ? 'Apps' : activeSheet === 'purwa' ? 'Purwatech Solutions' : activeSheet === 'projects' ? 'Projects' : 'Lainnya'}
				</span>
				<button onclick={closeSheet} class="p-1 rounded-lg hover:bg-slate-100 text-slate-400 cursor-pointer" aria-label="Tutup">
					<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
					</svg>
				</button>
			</div>

			<div class="p-3 space-y-1">
				{#if activeSheet === 'apps'}
					{#each appsItems as item}
						<a
							href={item.href}
							target="_blank"
							rel="noopener noreferrer"
							onclick={closeSheet}
							class="flex items-center justify-between p-3 rounded-xl hover:bg-indigo-50/70 transition"
						>
							<div>
								<p class="text-sm font-semibold text-slate-800">{item.title}</p>
								<p class="text-xs text-slate-500">{item.desc}</p>
							</div>
							<div class="flex items-center gap-2 shrink-0">
								{#if item.badge}
									<span class="px-2 py-0.5 text-[10px] font-semibold rounded-md bg-indigo-50 text-indigo-600 border border-indigo-100">{item.badge}</span>
								{/if}
								<svg class="w-3.5 h-3.5 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
								</svg>
							</div>
						</a>
					{/each}

				{:else if activeSheet === 'purwa'}
					{#each purwaItems as item}
						<a
							href={item.href}
							target="_blank"
							rel="noopener noreferrer"
							onclick={closeSheet}
							class="flex items-center justify-between p-3 rounded-xl hover:bg-indigo-50/70 transition"
						>
							<div>
								<p class="text-sm font-semibold text-slate-800">{item.title}</p>
								<p class="text-xs text-slate-500">{item.desc}</p>
							</div>
							<div class="flex items-center gap-2 shrink-0">
								{#if item.badge}
									<span class="px-2 py-0.5 text-[10px] font-semibold rounded-md bg-indigo-50 text-indigo-600 border border-indigo-100">{item.badge}</span>
								{/if}
								<svg class="w-3.5 h-3.5 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
									<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
								</svg>
							</div>
						</a>
					{/each}

				{:else if activeSheet === 'projects'}
					{#each projectItems as item}
						{#if item.children}
							<div class="p-3 rounded-xl bg-slate-50/80 space-y-1.5">
								<span class="text-sm font-bold text-slate-800">{item.title}</span>
								<p class="text-xs text-slate-500">{item.desc}</p>
								<div class="pl-3 border-l-2 border-indigo-200 space-y-1 mt-2">
									{#each item.children as sub}
										<a
											href={sub.href}
											target="_blank"
											rel="noopener noreferrer"
											onclick={closeSheet}
											class="flex items-center justify-between p-2 rounded-lg hover:bg-white transition text-sm"
										>
											<span class="font-medium text-slate-700">{sub.title}</span>
											{#if sub.badge}
												<span class="px-1.5 py-0.5 text-[9px] font-semibold rounded-md {sub.badge === 'Admin' ? 'bg-indigo-50 text-indigo-700 border border-indigo-200' : 'bg-emerald-50 text-emerald-700 border border-emerald-200'}">{sub.badge}</span>
											{/if}
										</a>
									{/each}
								</div>
							</div>
						{:else}
							<div class="flex items-center justify-between p-3 rounded-xl bg-slate-50/60 opacity-80">
								<div>
									<p class="text-sm font-semibold text-slate-700">{item.title}</p>
									<p class="text-xs text-slate-500">{item.desc}</p>
								</div>
								{#if item.badge}
									<span class="px-2 py-0.5 text-[10px] font-semibold rounded-md bg-amber-50 text-amber-700 border border-amber-200 shrink-0">{item.badge}</span>
								{/if}
							</div>
						{/if}
					{/each}

				{:else if activeSheet === 'more'}
					{#each moreItems as group}
						<div class="mb-3 last:mb-0">
							<div class="text-[11px] font-bold uppercase tracking-wider text-slate-400 px-2 mb-1.5">{group.label}</div>
							{#each group.items as item}
								{#if item.href && !item.isSoon}
									<a
										href={item.href}
										target={item.isExternal ? '_blank' : '_self'}
										rel={item.isExternal ? 'noopener noreferrer' : ''}
										onclick={closeSheet}
										class="flex items-center justify-between p-2.5 rounded-xl hover:bg-indigo-50/70 transition"
									>
										<span class="text-sm font-medium text-slate-700">{item.title}</span>
										<div class="flex items-center gap-1.5 shrink-0">
											{#if item.badge}
												<span class="px-1.5 py-0.5 text-[9px] font-semibold rounded-md bg-indigo-50 text-indigo-600 border border-indigo-100">{item.badge}</span>
											{/if}
											{#if item.isExternal}
												<svg class="w-3 h-3 text-slate-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
													<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
												</svg>
											{/if}
										</div>
									</a>
								{:else}
									<div class="flex items-center justify-between p-2.5 rounded-xl opacity-70">
										<span class="text-sm font-medium text-slate-500">{item.title}</span>
										{#if item.badge}
											<span class="px-1.5 py-0.5 text-[9px] font-semibold rounded-md bg-amber-50 text-amber-700 border border-amber-200">{item.badge}</span>
										{/if}
									</div>
								{/if}
							{/each}
						</div>
					{/each}
				{/if}
			</div>
		</div>
	</div>
{/if}

<nav class="fixed bottom-0 left-0 right-0 z-[100] lg:hidden bg-white/95 backdrop-blur-md border-t border-slate-200/80 shadow-[0_-2px_10px_rgba(0,0,0,0.06)]">
	<div class="flex items-center justify-around h-16 max-w-lg mx-auto px-2">
		<button
			onclick={(e) => { e.stopPropagation(); toggleSheet('apps'); }}
			class="flex flex-col items-center justify-center gap-0.5 min-w-[56px] py-1 rounded-xl transition cursor-pointer {activeSheet === 'apps' ? 'text-indigo-600' : 'text-slate-500 hover:text-slate-700'}"
		>
			<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zm10 0a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zm10 0a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z" />
			</svg>
			<span class="text-[10px] font-semibold">Apps</span>
		</button>

		<button
			onclick={(e) => { e.stopPropagation(); toggleSheet('purwa'); }}
			class="flex flex-col items-center justify-center gap-0.5 min-w-[56px] py-1 rounded-xl transition cursor-pointer {activeSheet === 'purwa' ? 'text-indigo-600' : 'text-slate-500 hover:text-slate-700'}"
		>
			<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 21V5a2 2 0 00-2-2H7a2 2 0 00-2 2v16m14 0h2m-2 0h-5m-9 0H3m2 0h5M9 7h1m-1 4h1m4-4h1m-1 4h1m-5 10v-5a1 1 0 011-1h2a1 1 0 011 1v5m-4 0h4" />
			</svg>
			<span class="text-[10px] font-semibold">Purwa</span>
		</button>

		<a
			href="/"
			onclick={closeSheet}
			class="flex flex-col items-center justify-center gap-0.5 min-w-[56px] py-1 rounded-xl transition {currentPath === '/' ? 'text-indigo-600' : 'text-slate-500 hover:text-slate-700'}"
		>
			<div class="w-10 h-10 rounded-full bg-gradient-to-tr from-indigo-600 to-blue-600 flex items-center justify-center text-white shadow-lg shadow-indigo-600/30 -mt-4">
				<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
				</svg>
			</div>
			<span class="text-[10px] font-semibold">Home</span>
		</a>

		<button
			onclick={(e) => { e.stopPropagation(); toggleSheet('projects'); }}
			class="flex flex-col items-center justify-center gap-0.5 min-w-[56px] py-1 rounded-xl transition cursor-pointer {activeSheet === 'projects' ? 'text-indigo-600' : 'text-slate-500 hover:text-slate-700'}"
		>
			<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z" />
			</svg>
			<span class="text-[10px] font-semibold">Projects</span>
		</button>

		<button
			onclick={(e) => { e.stopPropagation(); toggleSheet('more'); }}
			class="flex flex-col items-center justify-center gap-0.5 min-w-[56px] py-1 rounded-xl transition cursor-pointer {activeSheet === 'more' ? 'text-indigo-600' : 'text-slate-500 hover:text-slate-700'}"
		>
			<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z" />
			</svg>
			<span class="text-[10px] font-semibold">Lainnya</span>
		</button>
	</div>
</nav>
