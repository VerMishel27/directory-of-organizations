<template>
	<div class="popup" :class="{ popup_opened: isActiveDelPopup }">
			<div class="popup__container">
					<form method="post"
								class="popup__form"
								@submit.prevent="removeItem(event)">
							<h1 class="popup__title">Вы уверены?</h1>
							<div class="popup__block-button">
									<button class="popup__button popup__button_cancel"
													type="button"
													@click="closePopup()">
											Отмена
									</button>
									<button class="popup__button popup__button_submit" type="submit">Да</button>
							</div>
					</form>
			</div>
	</div>
</template>

<script>
	import './DelOrganizationPopup.css';

	export default {
			props: {
					isActiveDelPopup: {
							type: Boolean
					},

					removeItem: {
							type: Object
					},

					closePopup: {
							type: Object
					}
			}
	}
</script>