<template>
    <div>
        <base-dialog v-if="inputInvalid" title="Invalid Input" @close="comfirmError">
            <template #default>
                <p>Unfortunately, at least one input value is invalid. </p>
                <p> please check all input and make sure you enter at least a few characters into each input field.</p>
            </template>
            <template #actions>
                <!-- <base-button @click="comfirmError">Okey</base-button> -->
            </template>
        </base-dialog>
        <base-card>
            <form @submit.prevent="submitData">
                <div class="form-control">
                    <label for="">Title</label>
                    <input id="title" type="text" name="title" ref="titleInput">
                </div>
                <div class="form-control">
                    <label for="description">Description</label>
                    <textarea id="description" rows="3" name="description" ref="desInput"></textarea>
                </div>
                <div class="form-control">
                    <label for="link">Link</label>
                    <input id="link" rows="3" name="link" type="url" ref="linkInput">
                </div>
                <div>
                    <base-button type="submit">Add Resources</base-button>
                </div>
            </form>
        </base-card>
    </div>
</template>
<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseDialog from '../UI/BaseDialog.vue';
export default {
    components: { BaseDialog, BaseButton },
    inject: ['addResource'],
    data() {
        return {
            inputInvalid: false
        }
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.desInput.value;
            const enteredLink = this.$refs.linkInput.value;
            if (enteredTitle.trim() === '' || enteredDescription === '' || enteredLink === '') {
                this.inputInvalid = true
                return;
            }
            this.addResource(enteredTitle, enteredDescription, enteredLink);
        },
        comfirmError() {
            this.inputInvalid = false;
        }
    }
}
</script>
<style scoped>
label {
    font-weight: bold;
    display: block;
    margin-bottom: 0.5rem;
}

input,
textarea {
    display: block;
    width: 100%;
    font: inherit;
    padding: 0.15rem;
    border: 1px solid #ccc;
}

input:focus,
textarea:focus {
    outline: none;
    border-color: #3a0061;
    background-color: #f7ebff;
}

.form-control {
    margin: 1rem 0;
}
</style>