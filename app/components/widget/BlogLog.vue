<script setup lang="ts">
const { timeEstablished } = useAppConfig()

const blogLog = [
	{ label: '2025-08-17', value: '加入 萌ICP备 雾ICP备' },
	{ label: '2025-08-16', value: '加入 揪蝉' },
	{ label: '2024-04-19', value: '发布第一篇文章' },
	{ label: '2024-04-10', value: '迁移至 Nuxt' },
	{ label: '2023-04-23', value: '迁移至 Hexo 使用 Anzhiyu 主题' },
	{ label: timeEstablished, value: '博客建立' },
]
</script>

<template>
<BlogWidget card title="更新日志">
	<ZDlGroup size="large" :items="blogLog" />
</BlogWidget>
</template>
