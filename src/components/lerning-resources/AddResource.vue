<template>

    <base-dialog 
        v-if="inputIsInvalid"
        title="Invalid Input"
        @close="closePopUp"
    >
        <template #default>
            <p>
                Sorry, at least one input is invalid. Please check them.
            </p>
        </template>
        <template #actions>
            <base-button @click="closePopUp"> Okay </base-button>
        </template>
    </base-dialog>

    <base-card>

        <form @submit.prevent="submitData">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" name="title" id="title" ref="titleInput">
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea ref="descInput" rows="3" name="description" id="description"></textarea>
            </div>
            <div class="form-control">
                <label for="link">Link</label>
                <input type="text" name="link" id="link" ref="linkInput">
            </div>
            <div>
                <base-button type="submit">
                    Add Resource
                </base-button>
            </div>
        </form>


    </base-card>

</template>

<script>

export default {
    inject: [
        'addResource',
    ],
    data() {
        return {
            inputIsInvalid: false,
        }
    },
    methods: {
        submitData() {
            const enteredTitle = this.$refs.titleInput.value;
            const enteredDescription = this.$refs.descInput.value;
            const enteredLink = this.$refs.linkInput.value;

            if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === '') {
                this.inputIsInvalid = true;
                return;
            }
            this.addResource(enteredTitle, enteredDescription, enteredLink);
        },      
        closePopUp() {
            this.inputIsInvalid = false;
        },
    },



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