<script lang="ts">
	import * as Sidebar from "#lib/components/ui/sidebar/index.js";
	import AppSidebar from "./AppSidebar.svelte";

	let { children } = $props();
</script>

<svelte:head>
	<title>Quiz后台管理</title>
</svelte:head>

<div class="management-app">
	<header class="management-header">Quiz后台管理</header>
	<Sidebar.Provider
		class="management-body"
		style="--sidebar-width: 200px; --sidebar-width-mobile: 200px;"
	>
		<AppSidebar />
		<main class="management-main">
			{@render children()}
		</main>
	</Sidebar.Provider>
</div>

<style>
	:global(body) {
		min-height: 100%;
		margin: 0;
	}

	.management-app {
		min-height: 100vh;
		color: #2c3e50;
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}

	.management-header {
		display: flex;
		height: 60px;
		align-items: center;
		padding: 0 20px;
		background: rgb(238, 241, 246);
		font-size: 40px;
		line-height: 1;
	}

	:global(.management-body) {
		min-height: calc(100vh - 60px);
	}

	.management-main {
		min-width: 0;
		flex: 1;
		padding: 20px;
	}
</style>
