<template>
	<dialog class="modal" id="edoModal" aria-labelledby="modalTitle" @click="close">
		<div :class="`modal__content ${selection == 3 && 'overflow-scroll'}`" @click.stop>
			<header class="modal__header">
				<h5 class="modal__title" id="modalTitle">{{ title }}</h5>
				<form method="dialog">
					<CloseButton @click="close" />
				</form>
			</header>

			<slot></slot>
		</div>
	</dialog>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
	name: "SuperModal",

	setup() {
		return {};
	},
	props: {
		title: {
			type: String,
			required: false,
		},
		selection: {
			type: Number,
			required: false,
		}
	},
	methods: {
		close(): void {
			this.$emit("close");
		},
	},
});
</script>

<style lang="scss" scoped>
@import "../styles/mixins";

.modal {
	@include flex-center;

	background: url("/img/background/fog.png") repeat center center / cover;
	background-size: 150%;

	animation: bg-animation 30s linear infinite;

	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;

	width: 100vw;
	height: 100dvh;
	padding: 20px;

	z-index: 1000;

	@include desktop {
		background-size: 200%;
	}

	@include desktop-s {
		background-size: 250%;
	}

	@include desktop {
		background-size: 300%;
	}

	@include tablet-mobile-average {
		background-size: 400%;
	}

	@include mobile-tablet {
		background-size: 650%;
	}

	&__content {
		@include scrollbar-alt;

		background-color: var(--color-black);
		border-radius: var(--border-radius);

		width: 451px;
		max-height: 97%;

		padding: 40px;

		overflow: hidden;

		.modal__header {
			display: flex;
			align-items: center;
			justify-content: space-between;
			gap: 16px;

			margin-bottom: 16px;

			.modal__title {
				font: {
					size: 20px;
					weight: 500;
				}

				color: var(--color-white);
			}
		}

		&__text-container {
			display: flex;
			flex-direction: column;
			gap: 8px;
		}

		.modal__text {
			font: {
				size: 14px;
				weight: 400;
			}

			color: var(--color-light-dark-gray);
			letter-spacing: 0.25px;
			line-height: 106%;
		}
	}
}

.overflow-scroll {
	overflow-y: scroll;
}

@keyframes bg-animation {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}
</style>
