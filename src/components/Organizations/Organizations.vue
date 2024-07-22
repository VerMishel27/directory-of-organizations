<template>
	<main class="organizations">
			<section class="search-add-organization">
					<form class="search-add-organization__search-block">
							<div class="search-add-organization__label">
									<input type="text"
												 v-model="valueName"
												 placeholder="Найти по ФИО"
												 class="search-add-organization__search">
							</div>
					</form>
					<button type="button"
									@click="openPopup(isActiveAddPopup)"
									class="search-add-organization__add-button">
							Добавить
					</button>
			</section>
			<OrganizationsList :delIndexItem="delIndexItem"
												 :openDelPopup="openDelPopup"
												 :organizations="organizations"
												 :valueName="valueName"/>
	</main>
</template>

<script>
	import OrganizationsList from '../OrganizationsList/OrganizationsList.vue';
	import './Organizations.css';

	export default {
			components: {
					OrganizationsList
			},

			props: {
					organizations: {
							type: Object
					},

					openPopup: {
							type: Object
					},

					isActiveAddPopup: {
							type: Boolean
					},

					openDelPopup: {
							type: Object
					},

					delIndexItem: {
							type: Object
					}
			},

			data() {
					return {
							valueName: ''
					}
			}
	}
</script>