<template>
	<article class="field__container">
		<a v-if="showLink" href="#" target="_blank" class="field__link">Скачать шаблоны</a>
		<label for="fileUpload" class="field">
			<div class="field__img-container">
				<img src="/img/ico/file-upload.svg" alt="" />
				<p class="field__text field__text--white">{{ title }}</p>
			</div>
			<p class="field__text field__text--description">Можно перетащить его в эту рамку</p>
		</label>
		<input ref="fileInput" type="file" id="fileUpload" class="field__input" @change="onChange" />
	</article>
</template>

<script lang="ts">
export default defineComponent({
	name: "FileField",
});
</script>
<script setup lang="ts">
import { Ref, defineComponent, ref } from "vue";

const props = defineProps({
	showLink: {
		type: Boolean,
		default: false
	}
})

const emit = defineEmits(["onChange"]);
const fileInput: Ref<HTMLInputElement> = ref({} as HTMLInputElement);

const title: Ref<string> = ref("Добавить файл");

// Methods
const onChange = (e: any) => {
	title.value = e.target.files[0].name;
	emit("onChange", e.target.files[0]);
};
</script>

<style lang="scss" scoped>
@import "../../styles/mixins";
@import "../../styles/media";

.field {
	@include flex-center;
	flex-direction: column;
	gap: 4px;

	background-image: url("data:image/svg+xml,%3csvg width='100%25' height='100%25' xmlns='http://www.w3.org/2000/svg'%3e%3crect width='100%25' height='100%25' fill='none' stroke='%23CBCBCB59' stroke-width='4' stroke-dasharray='5' stroke-dashoffset='0' stroke-linecap='butt'/%3e%3c/svg%3e");

	padding: 10px;
	height: 100%;
	width: 100%;

	cursor: pointer;

	&__link {
		position: absolute;
		left: 50%;
		top: -20px;
		translate: -50% -50%;

		color: var(--color-light-dark-gray);
		text-decoration: underline;
	}

	&__container {
		background-color: var(--color-transparent-5-white);
		border-radius: var(--border-radius);

		padding: 16px;
		height: 108px;
		width: 100%;
		max-width: 600px;

		position: relative;
	}

	&__img-container {
		@include flex-center;
		gap: 12px;
	}

	&__text {
		font-size: 16px;
		line-height: 1;

		&--white {
			font-size: 14px;
			line-height: 18px;
			color: var(--color-white);
		}

		&--description {
			@include tablet-mobile-average {
				@include visually-hidden;
			}
		}
	}

	&__input {
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		opacity: 0;
		z-index: 2;
		cursor: pointer;
	}
}
</style>
