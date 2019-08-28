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
            console.log(this.zip);
            
        }
    }
}
</script>
