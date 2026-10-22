<script lang="ts">
	import { page } from "$app/state";
	import * as Collapsible from "#lib/components/ui/collapsible/index.js";
	import * as Sidebar from "#lib/components/ui/sidebar/index.js";

	const managementLinks = [
		{ href: "/manage/users", label: "用户管理" },
		{ href: "/manage/questions", label: "题目管理" }
	];
</script>

<Sidebar.Root side="left" variant="sidebar" collapsible="none" class="management-sidebar">
	<Sidebar.Content>
		<Sidebar.Group class="management-group">
			<Collapsible.Root open>
				<Collapsible.Trigger class="management-section-trigger">
					<span>管理选项</span>
					<span class="section-chevron" aria-hidden="true">v</span>
				</Collapsible.Trigger>
				<Collapsible.Content>
					<nav aria-label="管理选项">
						{#each managementLinks as link}
							<a
								href={link.href}
								class:active={page.url.pathname === link.href}
								aria-current={page.url.pathname === link.href ? "page" : undefined}
							>
								{link.label}
							</a>
						{/each}
					</nav>
				</Collapsible.Content>
			</Collapsible.Root>
		</Sidebar.Group>
	</Sidebar.Content>
</Sidebar.Root>

<style>
	:global(.management-sidebar) {
		--sidebar: rgb(238, 241, 246);
		--sidebar-foreground: #303133;
		width: 200px;
		min-width: 200px;
		border: 0;
		background: rgb(238, 241, 246);
	}

	:global(.management-group) {
		padding: 0;
	}

	:global(.management-section-trigger) {
		display: flex;
		width: 100%;
		height: 56px;
		align-items: center;
		justify-content: space-between;
		border: 0;
		padding: 0 20px;
		background: transparent;
		color: #303133;
		font: inherit;
		font-size: 14px;
		text-align: left;
		cursor: pointer;
	}

	.section-chevron {
		color: #909399;
		font-size: 14px;
	}

	nav a {
		display: flex;
		height: 56px;
		align-items: center;
		padding: 0 40px;
		color: #303133;
		font-size: 14px;
		text-decoration: none;
		transition: color 0.15s, background-color 0.15s;
	}

	nav a:hover {
		background: #e6e9ef;
	}

	nav a.active {
		color: #42b983;
	}
</style>
