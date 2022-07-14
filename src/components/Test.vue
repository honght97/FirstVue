<template>
    <div>
        Hello from {{lastName}} and {{isHello ? `${firsName}  ${lastName}` : ''}}
    </div>
    <button @click="onChangeName">Change Name</button>
    <div class="modal" v-if="isShowModal">
        <p>Modal content</p>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                firsName: "Hoang",
                lastName: "Hong",
                isHello: true,
                isShowModal: false,
            }
        },
        methods: {
            onChangeName() {
             this.firsName = "Thao";
             this.isShowModal = !this.isShowModal;
            }
        }
    }
</script>