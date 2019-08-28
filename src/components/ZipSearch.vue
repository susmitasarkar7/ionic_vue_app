<template>
    <ion-grid>
        <form @submit="onSubmit">
            <ion-col>
                <ion-item>
                    <ion-label>Zipcode: </ion-label>
                    <ion-input :value="Zip" @input="zip = $event.target.value"
                        placeholder="Enter Indian Zipcode" name="zip"></ion-input>
                </ion-item>
            </ion-col>
            <ion-col>
                <ion-button type="submit" color="primary" expand="block">Find</ion-button>
            </ion-col>
        </form>
    </ion-grid>
</template>

<script>
export default {
    name: "ZipSearch",
    data() {
        return {
            Zip: ""
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault();
            // Zip Regex
            const isValidZip = /^[1-9]{1}[0-9]{2}\s{0,1}[0-9]{3}$/.test(this.zip);
            // Test for valid zip
            if(!isValidZip) {
                this.showAlert();
                this.zip = "";
            } else {
                this.$emit("get-zip", this.zip);
                this.zip = "";
            }
        },
        showAlert() {
            return this.$ionic.alertController
                .create({
                    header: "Enter Zipcode",
                    message: "Please enter a valid Indian zipcode",
                    buttons: ["OK"]
                })
                .then(a => a.present());
        }
    }
}
</script>
