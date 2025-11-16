<script setup lang="ts">
const blogLog = [
	{ label: '2025-08-17', value: '加入 萌ICP备 雾ICP备' },
	{ label: '2025-08-16', value: '加入 揪蝉' },
	{ label: '2024-04-19', value: '发布第一篇文章' },
	{ label: '2024-04-10', value: '迁移至 Nuxt' },
	{ label: '2023-04-23', value: '迁移至 Hexo 使用 Anzhiyu 主题' },
	{ label: '2023-04-21', value: '博客建立' },
]
</script>

<template>
<ZWidget card title="更新日志">
	<div class="timeline">
		<div v-for="(item, index) in blogLog" :key="index" class="timeline-item">
			<div class="timeline-caption">{{ item.label }}</div>
			<div class="timeline-body">{{ item.value }}</div>
		</div>
	</div>
</ZWidget>
</template>

<style lang="scss" scoped>
.timeline {
	position: relative;
	font-size: 0.9em;

	&::before {
		content: "";
		position: absolute;
		inset: 0.5em auto 0;
		inset-inline-start: 0.5em;
		width: 0.3em;
		background-color: var(--c-bg-soft);
	}

	.timeline-item {
		position: relative;
	}
}

:deep() {
	.timeline-caption {
		position: relative;
		opacity: 0.8;
		margin-bottom: 0.2em;
		font-size: 0.9em;
		padding-inline-start: 1.5em;

		&::before {
			content: "";
			position: absolute;
			inset-inline-start: 0.3em;
			width: 0.8em;
			height: 0.8em;
			margin-top: 0.5em;
			border-radius: 1em;
			background-color: var(--c-text-2);
		}
	}

	.timeline-body {
		overflow: hidden;
		width: fit-content;
		margin-bottom: 1em;
		padding: 0 1em;
		margin-inline-start: 1em;
	}
}
</style>
