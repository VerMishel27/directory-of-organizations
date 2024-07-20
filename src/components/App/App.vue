<template>
    <div className="page">
        <Organizations :delIndexItem="delIndexItem" :organizations="organizations" :openPopup="openPopup" :openDelPopup="openDelPopup" :isActiveAddPopup="isActiveAddPopup" />
        <AddOrganizationPopup :organizations="organizations" :isActiveAddPopup="isActiveAddPopup"
            :closePopup="closePopup" :submitForm="submitForm" />
        <DelOrganizationPopup :closePopup="closePopup" :removeItem="removeItem" :isActiveDelPopup="isActiveDelPopup" />
    </div>
</template>

<script>
import './App.css'
import { ref } from 'vue';
import Organizations from '../Organizations/Organizations.vue'
import AddOrganizationPopup from '../AddOrganizationPopup/AddOrganizationPopup.vue'
import DelOrganizationPopup from '../DelOrganizationPopup/DelOrganizationPopup.vue'
// import Table from './Table.vue';

export default {

    components: { Organizations, AddOrganizationPopup, DelOrganizationPopup },

    data() {
        return {
            valueName: '',
            organizations: [
                {
                    name: 'ООО Вектор',
                    director: 'Васильев Д М',
                    number: '+79315086483'
                },
                {
                    name: 'ООО Вектор',
                    director: 'Васильев Д М',
                    number: '+79315086483'
                },
                {
                    name: 'ООО Вектор',
                    director: 'Васильев Д М',
                    number: '+79315086483'
                }
            ],
            isActiveAddPopup: false,
            // Отфильтрованный массив
            filterOrganizations: [],
            filterActive: false,
            isActiveDelPopup: false,
            isIndex: Number
        }
    },

    methods: {
        openPopup() {
            this.isActiveAddPopup = true
        },

        closePopup() {
            this.isActiveAddPopup = false;
            this.isActiveDelPopup = false;
        },

        openDelPopup() {
            this.isActiveDelPopup = true
        },

        delIndexItem(index) {
            this.isIndex = index
        },

        removeItem(event) {
            // event.preventDefault(),
            this.organizations.splice(this.isIndex, 1);
            this.isActiveDelPopup = false
        },
    },
    computed: {

    }
}
</script>
