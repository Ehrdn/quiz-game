<script lang="ts">
	import { Button } from "#lib/components/ui/button/index.js";
	import { Input } from "#lib/components/ui/input/index.js";

	const users = [
		{ date: "2016-05-01", name: "王小虎", password: "1234567" },
		{ date: "2016-05-01", name: "王小虎", password: "1234567" },
		{ date: "2016-05-01", name: "王小虎", password: "1234568" },
		{ date: "2016-05-01", name: "王小虎", password: "1234567" }
	];

	let username = $state("");
	let dialog: HTMLDialogElement;
</script>

<section aria-label="用户管理">
	<form class="search-form" onsubmit={(event) => event.preventDefault()}>
		<label class="field-label" for="user-search">用户名</label>
		<Input id="user-search" bind:value={username} placeholder="请输入用户名" class="search-input" />
		<Button type="submit" class="element-button primary-button">查询</Button>
		<Button type="button" class="element-button success-button" onclick={() => dialog.showModal()}>
			添加用户
		</Button>
	</form>

	<table class="management-table user-table">
		<thead>
			<tr>
				<th style="width: 180px;">日期</th>
				<th style="width: 180px;">姓名</th>
				<th style="width: 180px;">密码</th>
				<th>操作</th>
			</tr>
		</thead>
		<tbody>
			{#each users as user}
				<tr>
					<td>
						<svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-calendar float-left relative top-0.75 right-0.5" viewBox="0 0 16 16">
							<path d="M3.5 0a.5.5 0 0 1 .5.5V1h8V.5a.5.5 0 0 1 1 0V1h1a2 2 0 0 1 2 2v11a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V3a2 2 0 0 1 2-2h1V.5a.5.5 0 0 1 .5-.5M1 4v10a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V4z"/>
						</svg>{user.date}
					</td>
					<td>
						<span class="name-tag">{user.name}</span>
					</td>
					<td>
						<span class="name-tag">{user.password}</span>
					</td>
					<td class="actions">
						<Button type="button" class="element-button mini-button">编辑</Button>
						<Button type="button" class="element-button mini-button danger-button">删除</Button>
					</td>
				</tr>
			{/each}
		</tbody>
	</table>

	<nav class="pagination" aria-label="分页">
		<Button type="button" class="pager-button" aria-label="上一页">&lt;</Button>
		<Button type="button" class="pager-button current-page">1</Button>
		<Button type="button" class="pager-button">2</Button>
		<Button type="button" class="pager-button">3</Button>
		<Button type="button" class="pager-button">4</Button>
		<Button type="button" class="pager-button">5</Button>
		<span class="pager-ellipsis">…</span>
		<Button type="button" class="pager-button">100</Button>
		<Button type="button" class="pager-button" aria-label="下一页">&gt;</Button>
	</nav>
</section>

<dialog bind:this={dialog} class="add-dialog">
	<form method="dialog">
		<header class="dialog-header">添加新用户</header>
		<div class="dialog-body">
			<label class="dialog-field">
				<span>用户名</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>密码</span>
				<Input type="text" autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>确认密码</span>
				<Input type="text" autocomplete="off" />
			</label>
		</div>
		<footer class="dialog-footer">
			<Button type="submit" value="cancel" variant="outline" class="element-button">取 消</Button>
			<Button type="submit" value="confirm" class="element-button primary-button">确 定</Button>
		</footer>
	</form>
</dialog>

<style>
	.search-form {
		display: flex;
		align-items: center;
		gap: 10px;
		margin-bottom: 22px;
	}

	.field-label {
		margin-right: 2px;
		color: #606266;
		font-size: 14px;
	}

	:global(.search-input) {
		width: 180px;
		height: 40px;
		border-radius: 4px;
		font-family: inherit;
		font-size: 14px;
	}

	:global(.element-button) {
		height: 40px;
		border: 1px solid #dcdfe6;
		border-radius: 4px;
		padding: 0 20px;
		background: #fff;
		color: #606266;
		font-family: inherit;
		font-size: 14px;
		font-weight: 400;
	}

	:global(.primary-button) {
		border-color: #409eff;
		background: #409eff;
		color: #fff;
	}

	:global(.primary-button:hover) {
		background: #66b1ff;
	}

	:global(.success-button) {
		border-color: #67c23a;
		background: #67c23a;
		color: #fff;
	}

	:global(.success-button:hover) {
		background: #85ce61;
	}

	.management-table {
		border-collapse: collapse;
		color: #606266;
		font-size: 14px;
		text-align: left;
	}

	.user-table {
		width: 60%;
		min-width: 520px;
	}

	th,
	td {
		height: 48px;
		border-bottom: 1px solid #ebeef5;
		padding: 0 10px;
	}

	th {
		color: #909399;
		font-weight: 500;
	}
	
	.actions {
		white-space: nowrap;
	}

	:global(.mini-button) {
		height: 28px;
		margin-right: 10px;
		padding: 0 10px;
		font-size: 12px;
	}

	:global(.danger-button) {
		border-color: #fbc4c4;
		background: #fef0f0;
		color: #f56c6c;
	}

	.pagination {
		display: flex;
		align-items: center;
		gap: 6px;
		margin-top: 18px;
	}

	:global(.pager-button) {
		width: 30px;
		height: 28px;
		border: 0;
		border-radius: 3px;
		padding: 0;
		background: #f4f4f5;
		color: #606266;
		font-size: 13px;
	}

	:global(.current-page) {
		background: #409eff;
		color: #fff;
	}

	.pager-ellipsis {
		padding: 0 3px;
		color: #606266;
	}

	.add-dialog {
		width: min(50vw, 700px);
		border: 0;
		border-radius: 2px;
		padding: 0;
		color: #606266;
		font-family: inherit;
	}

	.add-dialog::backdrop {
		background: rgb(0 0 0 / 50%);
	}

	.dialog-header {
		border-bottom: 1px solid #ebeef5;
		padding: 20px;
		color: #303133;
		font-size: 18px;
	}

	.dialog-body {
		padding: 24px 20px 10px;
	}

	.dialog-field {
		display: grid;
		grid-template-columns: 90px 1fr;
		align-items: center;
		gap: 12px;
		margin-bottom: 18px;
		font-size: 14px;
	}

	.dialog-field :global(input) {
		height: 40px;
		border-radius: 4px;
		font-family: inherit;
		font-size: 14px;
	}

	.dialog-footer {
		display: flex;
		justify-content: flex-end;
		gap: 10px;
		border-top: 1px solid #ebeef5;
		padding: 12px 20px;
	}

	@media (max-width: 800px) {
		.user-table {
			width: 100%;
		}

		.add-dialog {
			width: calc(100vw - 32px);
		}
	}
</style>
