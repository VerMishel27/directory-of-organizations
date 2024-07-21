<template>
    <table className="organizations-list">
        <thead>
            <tr className="organizations-list__line organizations-list__line_border">
                <th className="organizations-list__column">Название</th>
                <th className="organizations-list__column"><a @click="sortedList()">ФИО директора</a></th>
                <th className="organizations-list__column">Номер телефона</th>
                <th className="organizations-list__column organizations-list__column_width"></th>
            </tr>
        </thead>
        <tbody>
            <tr className="organizations-list__line" v-if="organizations.length == 0">
                <td colspan="4" className="organizations-list__column">Список организаций пуст.</td>
            </tr>
            <tr className="organizations-list__line" v-for="(el, index) in filteredList.slice(number, quantity)"
                :key="index">
                <td className="organizations-list__column">{{ el.name }}</td>
                <td className="organizations-list__column">{{ el.director }}</td>
                <td className="organizations-list__column">{{ el.number }}</td>
                <td className="organizations-list__column organizations-list__column_width">
                    <button @click="removeItem(index)" type="button" className="organizations-list__button-close">
                        <img className="organizations-list__close-icon" src="../../images/del-icon.svg" alt="">
                    </button>
                </td>
            </tr>
        </tbody>
    </table>
    <div className="organizations-list__button-block">
        <button type="button" @click="pageBackSwitch()" className="organizations-list__button-back">
            <img className="organizations-list__icon-btn organizations-list__icon-btn_rotate"
                src="../../images/forward-icon.svg" alt="">

        </button>
        <p className="organizations-list__page-number">Страница {{ page }}</p>
        <button type="button" @click="pageSwitch()" className="organizations-list__button-forward">
            <img className="organizations-list__icon-btn" src="../../images/forward-icon.svg" alt="">

        </button>
    </div>
</template>

<script>
import { ref } from 'vue';
import './OrganizationsList.css'

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
            sortDirectors: 'directors',
            sortCompany: '',
            page: ref(1),
            number: 0,
            quantity: 10
        }
    },

    methods: {
        removeItem(index) {
            this.openDelPopup()
            this.delIndexItem(index)
            // this.organizations.splice(index, 1)
        },
        sortedList() {
            switch (this.sortParam) {
                case 'directors': return this.organizations.sort(sortByDirectors);
                default: return this.organizations;
            }
            // return this.organizations.sort(sortByDirectors)
        },

        pageSwitch() {
            if (this.organizations.length > 10 && this.organizations.length > this.quantity) {
                this.page++;
                this.number = this.number + 10
                this.quantity = this.quantity + 10
            }
            if (this.organizations.length <= 10 || this.organizations.length < this.quantity) {
                console.log('нельзя')
            }
        },

        pageBackSwitch() {
            if (this.organizations.length < 10 || this.page === 1) {
                console.log('нельзя понял')
            }
            if (this.organizations.length > 10 && this.page !== 1) {
                this.page--;
                this.number = this.number - 10;
                this.quantity = this.quantity - 10;
            }
        }
    },

    computed: {
        filteredList() {
            return this.organizations.filter((item) => {
                if (this.valueName === '') return true;
                else return item.director.toLowerCase().indexOf(this.valueName.toLowerCase()) > -1;
            })
        },
    }
}

const sortByDirectors = function (d1, d2) { return (d1.director.toLowerCase() > d2.director.toLowerCase()) ? 1 : -1; }
</script>