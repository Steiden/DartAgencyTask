<template>
	<div class="input__container">
		<input
			ref="input"
			:id="id"
			:type="type"
			class="input"
			:placeholder="placeholder"
			:disabled="disabled"ц
			:required="required"
			:value="value"
			@input="onChange"
		/>
		<label :for="id" class="input__label"
			>{{ placeholder }} <span class="input__span"> – введите корректное значение</span></label
		>
		<img src="../../assets/svg/error.svg" class="input__error-icon" />
	</div>
</template>

<script lang="ts">
import { Ref, defineComponent, ref } from "vue";

export default defineComponent({
	setup() {
		const input: Ref<HTMLInputElement> = ref({} as HTMLInputElement);

		return {
			input
		}
	},
	name: "CustomInput",
	props: {
		id: {
			type: String,
			required: false,
		},
		type: {
			type: String,
			default: "text",
		},
		placeholder: {
			type: String,
			default: "",
		},
		disabled: {
			type: Boolean,
			default: false,
		},
		required: {
			type: Boolean,
			default: false,
		},
		value: {
			type: String,
			default: "",
		},
		onChange: {
			type: Object as () => (e: any) => void,
			default: () => {},
		}
	}
});
</script>

<style lang="scss" scoped>
@import "../../styles/mixins";

.input {
	$height: 47;

	background-color: var(--color-light-black);
	color: var(--color-dark-alt-gray);

	border: var(--border);
	border-radius: var(--border-radius);

	height: #{$height}px;
	padding-inline: 16px;

	// min-width: 280px;

	@include mobile-tablet {
		min-width: 100%;
	}

	&::placeholder {
		color: var(--color-dark-alt-gray);
	}

	&:focus {
		border-color: var(--color-white);
		color: var(--color-white);
	}

	&:not(:focus) {
		& + .input__label {
			display: none;
		}
	}

	&:disabled {
		background-color: var(--color-light-alt-black);
		border-color: var(--color-transparent-10-white);

		&::placeholder {
			color: var(--color-dark-alt-gray);
		}
	}

	&:user-invalid {
		border-color: var(--color-alt-red);

		& + .input__label {
			display: block;
		}
	}

	&:not(:user-invalid) {
		& + .input__label > .input__span,
		& + .input__label + .input__error-icon {
			display: none;
		}
	}

	&__container {
		display: flex;
		flex-direction: column-reverse;
		gap: 4px;

		position: relative;
	}

	&__label {
		font: {
			size: 12px;
			weight: 400;
		}
		color: var(--color-light-dark-alt-gray);
		letter-spacing: 0.25px;

		position: absolute;
		top: -4px;
		left: 0;
		translate: 0 -100%;
	}

	&__span {
		font: {
			size: 12px;
			weight: 400;
		}
		color: var(--color-alt-red);
		line-height: 0.25px;

		position: relative;
	}

	&__error-icon {
		position: absolute;
		bottom: #{calc($height / 2)}px;
		right: 6px;
		translate: 0 50%;

		width: 20px;
		height: 20px;
	}
}
</style>
