<template>
	<div class="selection">
		<div class="selection__content">
			<div class="modal__text-container selection__text-container">
				<p class="selection__text modal__text">
					Вы можете подключить услугу, выбрав в поле ответ «Хочу установить». С Вами свяжется наш
					менеджер и объяснит, как происходит процедура подключения.
				</p>
				<p class="selection__text modal__text">
					Если же Вы не намерены в ближайшее время подключать ЭДО, тогда не заполняйте форму дальше.
				</p>
			</div>

			<CustomButton
				class="selection__button modal__button"
				@click="
					{
						close();
						$router.push({ name: 'EdoNo' });
					}
				"
				>Понятно</CustomButton
			>
		</div>

		<img src="../../../assets/svg/smile.svg" class="selection__image" />
	</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
	name: "SelectionNo",

	setup() {
		return {};
	},
	methods: {
		close() {
			this.$emit("close");
		},
	},
	mounted() {
		this.$router.push({ name: "Form" });
	}
});
</script>

<style lang="scss" scoped>
.selection {
	position: relative;

	&__content {
		display: flex;
		flex-direction: column;
		align-items: center;

		position: relative;
		overflow: hidden;
		z-index: 2;
	}

	&__image {
		position: absolute;
		bottom: -100px;
		left: -125px;
		z-index: 1;
	}

	&__button {
		margin-top: 40px;
		padding-inline: 55px;
	}
}
</style>
