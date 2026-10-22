<script lang="ts">
	import { Button } from "#lib/components/ui/button/index.js";
	import { Input } from "#lib/components/ui/input/index.js";

	const questions = Array.from({ length: 4 }, (_, index) => ({
		id: String(index + 1),
		question: "法国的首都是哪个城市？",
		options: "巴黎 巴黎 巴黎 巴黎",
		answer: "巴黎"
	}));

	let keyword = $state("");
	let dialog: HTMLDialogElement;
</script>

<section aria-label="题目管理">
	<form class="search-form" onsubmit={(event) => event.preventDefault()}>
		<label class="field-label" for="question-search">题目</label>
		<Input
			id="question-search"
			bind:value={keyword}
			placeholder="请输入题目关键词"
			class="search-input"
		/>
		<Button type="submit" class="element-button primary-button">查询</Button>
		<Button type="button" class="element-button success-button" onclick={() => dialog.showModal()}>
			添加题目
		</Button>
	</form>

	<table class="management-table question-table">
		<thead>
			<tr>
				<th style="width: 50px;">序号</th>
				<th style="width: 250px;">题目</th>
				<th style="width: 260px;">选项</th>
				<th style="width: 180px;">答案</th>
				<th>操作</th>
			</tr>
		</thead>
		<tbody>
			{#each questions as question}
				<tr>
					<td>{question.id}</td>
					<td>{question.question}</td>
					<td>{question.options}</td>
					<td>{question.answer}</td>
					<td class="actions">
						<Button type="button" class="element-button mini-button">编辑</Button>
						<Button type="button" class="element-button mini-button danger-button">删除</Button>
					</td>
				</tr>
			{/each}
		</tbody>
	</table>

	<nav class="pagination" aria-label="分页">
		<Button type="button" class="pager-button" aria-label="上一页">‹</Button>
		<Button type="button" class="pager-button current-page">1</Button>
		<Button type="button" class="pager-button">2</Button>
		<Button type="button" class="pager-button">3</Button>
		<Button type="button" class="pager-button">4</Button>
		<Button type="button" class="pager-button">5</Button>
		<span class="pager-ellipsis">…</span>
		<Button type="button" class="pager-button">100</Button>
		<Button type="button" class="pager-button" aria-label="下一页">›</Button>
	</nav>
</section>

<dialog bind:this={dialog} class="add-dialog">
	<form method="dialog">
		<header class="dialog-header">添加题目</header>
		<div class="dialog-body">
			<label class="dialog-field">
				<span>题目</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>选项A</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>选项B</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>选项C</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>选项D</span>
				<Input autocomplete="off" />
			</label>
			<label class="dialog-field">
				<span>答案</span>
				<Input autocomplete="off" />
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
		width: 230px;
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

	.question-table {
		width: 80%;
		min-width: 1000px;
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
		.question-table {
			width: 100%;
		}

		.add-dialog {
			width: calc(100vw - 32px);
		}
	}
</style>
