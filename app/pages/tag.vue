<script setup lang="ts">
import type ArticleProps from '~/types/article'
import { sort } from 'radash'

const appConfig = useAppConfig()
useSeoMeta({
	title: '标签',
	description: `${appConfig.title}的所有文章标签。`,
})

const layoutStore = useLayoutStore()
layoutStore.setAside(['blog-stats', 'blog-tech'])

const { data: listRaw } = await useAsyncData<ArticleProps[]>('tags-articles', () =>
	useArticleIndex().then(data => data.data.value))

const articlesByTag = computed(() => {
	const result: Record<string, ArticleProps[]> = {}
	const articles = sort(listRaw.value || [], a => new Date(a.date || 0).getTime(), true)
	for (const article of articles) {
		if (article.tags) {
			for (const tag of article.tags) {
				if (!result[tag]) {
					result[tag] = []
				}
				result[tag].push(article)
			}
		}
	}
	return result
})

const sortedTags = computed(() => {
	return Object.keys(articlesByTag.value).sort((a, b) => {
		const aCount = articlesByTag.value[a]?.length || 0
		const bCount = articlesByTag.value[b]?.length || 0
		return bCount - aCount
	})
})
</script>

<template>
<div class="tag proper-height">
	<section
		v-for="tag in sortedTags"
		:key="tag"
		class="tag-group"
	>
		<div class="tag-title">
			<h2 class="tag-name">
				{{ tag }}
			</h2>

			<div class="tag-info">
				<span>{{ articlesByTag[tag]?.length }}篇</span>
			</div>
		</div>

		<TransitionGroup tag="menu" class="tag-list" name="float-in">
			<ZArchive
				v-for="article, index in articlesByTag[tag]"
				:key="article.path"
				v-bind="article"
				:to="article.path"
				:style="{ '--delay': `${index * 0.03}s` }"
			/>
		</TransitionGroup>
	</section>
</div>
</template>

<style lang="scss" scoped>
.tag {
	margin: 1rem;
	mask-image: linear-gradient(#FFF 50%, #FFF5);
}

.tag-group {
	margin: 1rem 0 3rem;
}

.tag-title {
	display: flex;
	justify-content: space-between;
	gap: 1em;
	position: sticky;
	opacity: 0.5;
	top: 0;
	font-size: min(1.5em, 5vw);
	color: transparent;
	transition: color 0.2s;

	&::selection, :hover > & {
		color: var(--c-text-3);
	}

	> .tag-name, .tag-info {
		margin-bottom: -0.3em;
		mask-image: linear-gradient(#FFF 50%, transparent);
		font-family: var(--font-stroke-free);
		font-size: 3em;
		font-variant-numeric: tabular-nums;
		font-weight: 800;
		line-height: 1;
		z-index: -1;
		-webkit-text-stroke: 1px var(--c-text-3);
	}

	> .tag-info {
		position: absolute;
		inset-inline-end: 0;
		transition: opacity 0.2s;
	}
}
</style>
