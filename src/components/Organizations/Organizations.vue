<template>
    <main className="organizations">
        <section className="search-add-organization">
            <form className="search-add-organization__search-block">
                <div className="search-add-organization__label">
                    <input type="text" v-model="valueName" placeholder="Найти по ФИО"
                        className="search-add-organization__search">
                </div>
            </form>
            <button type="button" @click="openPopup(isActiveAddPopup)" className="search-add-organization__add-button">Добавить</button>
        </section>
        <OrganizationsList :delIndexItem="delIndexItem" :openDelPopup="openDelPopup" :organizations="organizations" :valueName="valueName" />
    </main>
</template>
<script>
import OrganizationsList from '../OrganizationsList/OrganizationsList.vue';
// import SearchAddOrganization from '../SearchAddOrganization/SearchAddOrganization.vue';
import './Organizations.css'

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