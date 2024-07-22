<template>
	<table class="organizations-list">
			<thead>
			<tr class="organizations-list__line organizations-list__line_border">
					<th class="organizations-list__column">
							<a class="organizations-list__filter-button"
								 @click="sortedList('company')">
									Название
							</a>
					</th>
					<th class="organizations-list__column">
							<a class="organizations-list__filter-button"
								 @click="sortedList('directors')">
									ФИО директора
							</a>
					</th>
					<th class="organizations-list__column">Номер телефона</th>
					<th class="organizations-list__column organizations-list__column_width"></th>
			</tr>
			</thead>
			<tbody>
			<tr class="organizations-list__line" v-if="organizations.length == 0">
					<td colspan="4" class="organizations-list__column">Список организаций пуст.</td>
			</tr>
			<tr class="organizations-list__line"
					v-for="(el, index) in filteredList.slice(number, quantity)" :key="index">
					<td class="organizations-list__column">{{ el.name }}</td>
					<td class="organizations-list__column">{{ el.director }}</td>
					<td class="organizations-list__column">{{ el.number }}</td>
					<td class="organizations-list__column organizations-list__column_width">
							<button @click="removeItem(index)"
											type="button"
											class="organizations-list__button-close">
									<img class="organizations-list__close-icon"
											 src="../../images/del-icon.svg"
											 alt="Удалить">
							</button>
					</td>
			</tr>
			</tbody>
	</table>
	<div class="organizations-list__button-block">
			<button :disabled="disableBackButton"
							type="button"
							@click="pageBackSwitch()"
							class="organizations-list__button-back"
							:class="{ button_disable: disableBackButton }">
					<img class="organizations-list__icon-btn organizations-list__icon-btn_rotate"
							 :class="{ icon_disable: disableBackButton }"
							 src="../../images/forward-icon.svg"
							 alt="Назад">
					<img src="../../images/forward-icon-disabled.svg"
							 alt="Назад"
							 class="organizations-list__icon-btn organizations-list__icon-btn_rotate"
							 :class="{ icon_disable: !disableBackButton }">
			</button>
			<p class="organizations-list__page-number">Страница {{ page }}</p>
			<button :disabled="!disableForwardButton"
							type="button"
							@click="pageSwitch()"
							class="organizations-list__button-forward"
							:class="{ button_disable: !disableForwardButton }">
					<img class="organizations-list__icon-btn"
							 :class="{ icon_disable: !disableForwardButton }"
							 src="../../images/forward-icon.svg"
							 alt="Вперед">
					<img src="../../images/forward-icon-disabled.svg"
							 alt="Вперед"
							 class="organizations-list__icon-btn"
							 :class="{ icon_disable: disableForwardButton }">
			</button>
	</div>
</template>

<script>
	import {ref} from 'vue';
	import './OrganizationsList.css';

	export default {

			props: {
					organizations: {
							type: Object
					},

					valueName: {
							type: String
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
							sortCompany: '',
							page: ref(1),
							number: 0,
							quantity: 10
					}
			},

			methods: {
					removeItem(index) {
							this.openDelPopup();
							this.delIndexItem(index);
					},

					sortedList(name) {
							switch (name) {
									case 'directors':
											return this.organizations.sort(sortByDirectors);
									case 'company':
											return this.organizations.sort(sortByCompany);
									default:
											return this.organizations;
							}
					},

					pageSwitch() {
							if (this.organizations.length > this.quantity) {
									this.page++;
									this.number = this.number + 10;
									this.quantity = this.quantity + 10;
							}
					},

					pageBackSwitch() {
							if (this.page !== 1) {
									this.page--;
									this.number = this.number - 10;
									this.quantity = this.quantity - 10;
							}
					},
			},

			computed: {
					filteredList() {
							return this.organizations.filter((item) => {
									if (this.valueName === '') return true;
									else return item.director.toLowerCase().indexOf(this.valueName.toLowerCase()) > -1;
							});
					},

					disableBackButton() {
							return this.page === 1;
					},

					disableForwardButton() {
							return this.organizations.length > this.quantity;
					}
			}
	}

	const sortByDirectors = function (d1, d2) {
			return (d1.director.toLowerCase() > d2.director.toLowerCase()) ? 1 : -1;
	};
	const sortByCompany = function (d1, d2) {
			return (d1.name.toLowerCase() > d2.name.toLowerCase()) ? 1 : -1;
	};
</script>