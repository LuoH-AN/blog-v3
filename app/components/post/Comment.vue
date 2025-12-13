<script setup lang="ts">
const appConfig = useAppConfig()

onMounted(() => {
	window.twikoo?.init?.({
		envId: appConfig.twikoo?.envId,
		el: '#twikoo',
	})
})
</script>

<template>
<section class="z-comment">
	<h3 class="text-creative">
		评论区
	</h3>
	<div id="twikoo">
		<div class="comment-loading">
			<div class="loading-spinner" />
			<p>评论加载中...</p>
		</div>
	</div>
</section>
</template>

<style lang="scss" scoped>
.z-comment {
	margin: 3rem 1rem;

	> h3 {
		margin-top: 3rem;
		font-size: 1.25rem;
	}
}

:deep(#twikoo) {
	margin: 2em 0;

	.tk-admin-container {
		position: fixed;
		z-index: calc(var(--z-index-popover) + 1);
	}

	.tk-input {
		font-family: var(--font-monospace);
	}

	@supports (corner-shape: squircle) {
		.tk-avatar {
			border-radius: 50%;
			corner-shape: superellipse(1.2);
		}
	}

	.tk-time {
		color: var(--c-text-3);
	}

	.tk-content {
		margin-top: 0;
	}

	.tk-expand {
		padding: 0.375rem 1rem;
		border-radius: 0.5rem;
		background-color: var(--c-bg-2);
		color: var(--c-text-1);
		transition: background-color 0.1s;

		&:hover {
			background-color: var(--c-bg-3);
		}
	}

	.tk-preview,
	.tk-cancel,
	.tk-send {
		border-radius: 8px;
	}

	.tk-comments-title, .tk-nick > strong {
		font-family: var(--font-creative);
	}

	.tk-owo-emotion {
		width: auto;
		height: 1.4em;
		vertical-align: text-bottom;
	}

	.tk-extras, .tk-footer {
		font-size: 0.7rem;
		color: var(--c-text-3);
	}

	.tk-replies:not(.tk-replies-expand) {
		mask-image: linear-gradient(#FFF 50%, transparent);
	}
}

:deep(:where(.tk-preview-container,.tk-content)) {
	pre {
		overflow: auto;
		border-radius: 0.5rem;
		font-size: 0.8125rem;
	}

	p {
		margin: 0.2em 0;
	}

	img {
		border-radius: 0.5em;
	}

	menu, ol, ul {
		margin: 0.5em 0;
		padding-inline-start: 1.5em;
		font-size: 0.9rem;
		list-style: revert;

		> li {
			margin: 0.2em 0;

			&::marker {
				color: var(--c-primary);
			}
		}
	}

	blockquote {
		margin: 0.5em 0;
		padding: 0.2em 0.5em;
		border-inline-start: 4px solid var(--c-border);
		border-radius: 4px;
		background-color: var(--c-bg-2);
		font-size: 0.9rem;
	}

	a {
		margin: 0 -0.1em;
		padding: 0 0.1em;
		background: linear-gradient(var(--c-primary-soft), var(--c-primary-soft)) no-repeat bottom/100% 0.1em;
		color: var(--c-primary);
		transition: all 0.2s;

		&:hover {
			border-radius: 0.3em;
			background-size: 100% 100%;
		}
	}
}
</style>
