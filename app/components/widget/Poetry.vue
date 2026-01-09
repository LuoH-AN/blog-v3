<script setup lang="ts">
interface PoetryData {
	content: string
	origin: {
		title: string
		author: string
		dynasty: string
	}
}

const poetry = ref<PoetryData | null>(null)
const loading = ref(true)

onMounted(() => {
	// @ts-expect-error jinrishici SDK
	if (typeof jinrishici !== 'undefined') {
		// @ts-expect-error jinrishici SDK
		jinrishici.load((result) => {
			if (result.status === 'success') {
				poetry.value = {
					content: result.data.content,
					origin: {
						title: result.data.origin.title,
						author: result.data.origin.author,
						dynasty: result.data.origin.dynasty,
					},
				}
			}
			loading.value = false
		})
	}
	else {
		loading.value = false
	}
})
</script>

<template>
<BlogWidget card title="今日诗词">
	<div v-if="loading" class="poetry-loading">
		加载中...
	</div>
	<div v-else-if="poetry" class="poetry-content">
		<div class="poetry-line">
			{{ poetry.content }}
		</div>
		<div class="poetry-info">
			<span class="poetry-title">《{{ poetry.origin.title }}》</span>
			<span class="poetry-author">
				{{ poetry.origin.dynasty }} • {{ poetry.origin.author }}
			</span>
		</div>
	</div>
	<div v-else class="poetry-error">
		诗词加载失败
	</div>
</BlogWidget>
</template>

<style lang="scss" scoped>
.poetry-loading,
.poetry-error {
	padding: 0.5rem;
	font-size: 0.9em;
	text-align: center;
	color: var(--c-text-3);
}

.poetry-content {
	.poetry-line {
		margin-bottom: 0.8rem;
		font-size: 1.1em;
		line-height: 1.8;
		text-align: center;
		color: var(--c-text-1);
	}

	.poetry-info {
		font-size: 0.85em;
		text-align: center;
		color: var(--c-text-3);

		.poetry-title {
			margin-right: 0.5em;
		}

		.poetry-author {
			font-style: italic;
		}
	}
}
</style>
