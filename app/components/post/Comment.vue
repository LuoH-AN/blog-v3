<script setup lang="ts">
const appConfig = useAppConfig()

onMounted(() => {
	window.twikoo?.init({
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
	margin: 2rem auto;
	padding: 0 1rem;

	h3 {
		margin-top: 3rem;
		font-size: 1.25rem;
	}
}

.comment-loading {
	padding: 2rem;
	text-align: center;
	color: var(--c-text-2);

	.loading-spinner {
		width: 40px;
		height: 40px;
		margin: 0 auto 1rem;
		border: 3px solid var(--c-bg-3);
		border-top-color: var(--c-primary);
		border-radius: 50%;
		animation: spin 1s linear infinite;
	}

	p { font-size: 0.9rem; }
}

:deep(#twikoo > :not(.tk-admin-container)) {
	.tk-avatar {
		overflow: hidden;
		border-radius: 50% !important;
	}

	.tk-submit {
		display: flex;
		flex-direction: column;

		.tk-avatar,
		a.tk-submit-action-icon.__markdown { display: none; }

		.tk-preview-container { margin-bottom: 0.5rem;
			margin-left: 0; }

		.tk-row.actions {
			justify-content: flex-end;
			order: 3;
			margin: 0 0 0.5rem;
		}

		.tk-input {
			order: 1;
			margin-bottom: 0.5rem;

			.el-textarea__inner {
				padding: 0.8rem;
				border: 2px solid var(--c-border);
				border-radius: 12px;
				background-color: var(--c-bg-2);
				transition: all 0.2s;

				&:focus {
					border-color: var(--c-primary);
					background-color: var(--c-bg);
					background-position-y: 350px;
				}
			}
		}

		.tk-meta-input {
			order: 2;
			position: relative;

			.el-input-group {
				border: 2px solid var(--c-border);
				border-radius: 10px;
				background: var(--c-bg-2);
				transition: all 0.2s;

				&:focus-within {
					border-color: var(--c-primary);
					background: var(--c-bg);

					&::before,
					&::after { display: block;
						animation: fadeInTip 0.3s ease; }
				}

				&::before {
					display: none;
					position: absolute;
					top: -60px;
					left: 50%;
					padding: 0.8rem 1rem;
					border: 1px solid var(--c-border);
					border-radius: 8px;
					background: var(--c-bg);
					font-size: 0.9rem;
					white-space: nowrap;
					color: var(--c-text-1);
					transform: translate(-50%);
					z-index: 100;
				}

				&::after {
					content: "";
					display: none;
					position: absolute;
					top: -12px;
					left: 50%;
					border: 8px solid transparent;
					border-top: 8px solid var(--c-bg);
					transform: translate(-50%);
				}
			}

			.el-input-group:first-child::before { content: "输入QQ号会自动获取昵称和头像🐧"; }
			.el-input-group:nth-child(2)::before { content: "收到回复将会发送到您的邮箱📧"; }
			.el-input-group:nth-child(3)::before { content: "可以通过昵称访问您的网站🔗"; }

			.el-input__inner { border: none !important; }

			.el-input-group__prepend {
				border: none;
				border-radius: 8px 0 0 8px;
				background: var(--c-bg-1);
				color: var(--c-text-2);
				transition: all 0.2s;
			}
		}
	}

	.OwO .OwO-body {
		border-radius: 8px;
		background: var(--c-bg);
		transform: translateZ(0);
		animation: fadeInPanel 0.3s ease 0.1s 1 normal both;
	}

	.tk-content {
		font-size: 0.95rem;
		line-height: 1.6;

		.tk-owo-emotion { width: auto;
			height: 1.4em;
			vertical-align: text-bottom; }

		a {
			margin: 0 -0.1em;
			padding: 0 0.1em;
			background: linear-gradient(var(--c-primary-soft), var(--c-primary-soft)) no-repeat bottom/100% 0.1em;
			color: var(--c-primary);
			transition: all 0.2s;

			&:hover { border-radius: 0.3em;
				background-size: 100% 100%; }
		}

		p > code,
		> code {
			padding: 0.2em 0.4em;
			border: 1px solid var(--c-border);
			border-radius: 6px;
			background: var(--c-bg-2);
		}

		.code-toolbar,
		> span > pre {
			position: relative;
			overflow: auto;
			padding: 0.4rem;
			border: 2px solid var(--c-border);
			border-radius: 8px;
			background: var(--c-bg-2);

			&::before { display: none; }

			pre {
				margin-top: 0.75rem;

				code { display: block;
					padding-top: 0.75rem; }
			}
		}

		blockquote {
			margin-bottom: 0.8rem;
			padding: 0.8rem;
			border-left: 4px solid var(--c-border);
			border-radius: 8px;
			background: var(--c-bg-2);
			color: var(--c-text-2);
			transition: all 0.2s;
		}
	}

	.tk-comments-title { margin-bottom: 0; }

	.tk-replies:not(.tk-replies-expand) {
		mask: linear-gradient(#FFF 50%, transparent);
		mask: linear-gradient(#FFF 50%, transparent);
	}

	.tk-expand {
		padding: 0.375rem 1rem;
		border-radius: 0.5rem;
		background-color: var(--c-bg-2);
		color: var(--c-text-1);
		transition: background-color 0.1s;

		&:hover { background-color: var(--c-bg-3); }
	}

	.tk-nick-link { color: var(--c-primary); }

	.tk-comment .tk-main {
		.tk-meta { margin-bottom: 0.3rem; }

		.tk-extras {
			margin-top: 0.5rem;
			font-size: 0.85rem;
			color: var(--c-text-2);
		}

		.tk-action .tk-action-link:first-child { display: none; }
	}

	.tk-preview,
	.tk-cancel {
		border: 1px solid var(--c-border);
		border-radius: 8px;
		background-color: var(--c-bg-2);
		color: var(--c-text-1);

		&:hover {
			border-color: var(--c-primary);
			background-color: var(--c-bg-3);
		}
	}

	.tk-send {
		border: 1px solid var(--c-primary);
		border-radius: 8px;
		background-color: var(--c-primary);
		color: white;

		&:hover {
			border-color: var(--c-primary-soft);
			background-color: var(--c-primary-soft);
		}
	}
}

@keyframes spin {
	0% { transform: rotate(0); }
	100% { transform: rotate(1turn); }
}

@keyframes fadeInTip {
	from { opacity: 0;
		transform: translate(-50%, 10px); }

	to { opacity: 1;
		transform: translate(-50%); }
}

@keyframes fadeInPanel {
	from { opacity: 0;
		transform: translateY(-20px); }

	to { opacity: 1;
		transform: translateY(0); }
}

:deep(#twikoo > :not(.tk-admin-container)) {
	.tk-submit .tk-avatar {
		display: block !important;
		order: 0;
		width: 48px;
		height: 48px;
		margin: 0 0.75rem 0 0 !important;
	}

	.tk-submit .tk-row.head {
		display: flex;
		align-items: flex-start;
		order: 1;
		width: 100%;
	}

	.tk-submit .tk-input {
		order: 1;
	}

	.tk-submit .tk-meta-input {
		order: 2;
	}

	.tk-submit .tk-row.actions {
		order: 3;
	}
}
</style>
