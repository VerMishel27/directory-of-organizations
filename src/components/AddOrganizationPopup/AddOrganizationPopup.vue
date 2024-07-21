<template>
    <div class="popup" :class="{ popup_opened: isActiveAddPopup }">
        <div class="popup__container">
            <form class="form" method="post" id="add-form" @submit.prevent="submitForm">
                <h1 class="form__title">Добавить организацию</h1>
                <div class="form__data">
                    <label for="" class="form__label">
                        <input name="name" required minlength="2" maxlength="30" type="text" placeholder="Название организации"
                            v-model="organizationName" class="form__input">
                    </label>
                    <label for="" class="form__label">
                        <input name="number" type="tel" required minlength="11" maxlength="11" placeholder="Номер телефона"
                            v-model.number="organizationNumber" class="form__input">
                    </label>
                    <label for="" class="form__label">
                        <input name="nameDirector" required type="text" minlength="2" maxlength="30" placeholder="ФИО директора"
                            v-model="organizationDirector" class="form__input">
                    </label>
                </div>
                <div class="form__block-button">
                    <button class="form__button form__button_cancel" @click="closeAddPopup()" type="button">Отмена</button>
                    <button  class="form__button form__button_submit"
                        type="submit">Ок</button>
                </div>
            </form>
        </div>
    </div>

</template>

<script>
import './AddOrganizationPopup.css'

export default {
    props: {
        isActiveAddPopup: {
            type: Boolean
        },

        closePopup: {
            type: Object
        },
        organizations: {
            type: Object
        }
    },

    data() {
        return {
            organizationName: '',
            organizationDirector: '',
            organizationNumber: ''
        }
    },

    methods: {
        submitForm(event) {
            event.preventDefault(),

                this.organizations.push({
                    name: this.organizationName,
                    director: this.organizationDirector,
                    number: this.organizationNumber
                })

            this.closePopup()
            this.organizationName = '',
            this.organizationDirector = '',
            this.organizationNumber = ''
        },

        closeAddPopup() {
            this.closePopup()
            this.organizationName = '',
            this.organizationDirector = '',
            this.organizationNumber = ''
        }
    },

    computed: {
    }
}
</script>