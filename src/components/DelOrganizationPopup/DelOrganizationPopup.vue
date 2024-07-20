<template>
    <div class="popup" :class="{ popup_opened: isActiveDelPopup}">
        <div className="popup__container">
            <form method="post" className="popup__form" @submit.prevent="removeItem(event)">
                <h1 className="popup__title">Вы уверены?</h1>
                <div className="popup__block-button">
                    <button className="popup__button popup__button_cancel"  type="button" @click="closePopup()">Отмена</button>
                    <button className="popup__button popup__button_submit" type="submit">Да</button>
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import './DelOrganizationPopup.css'

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