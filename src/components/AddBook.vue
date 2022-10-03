<template>
    <!-- form to add book -->
    <form @submit.prevent="addBook()" id="form">
        <h3 class="title is-3">Lägg till ny bok</h3>
        <br>
        <div class="field">
            <label class="label">Titel</label>
            <div class="control">
                <input v-model="title" class="input" type="text" placeholder="">
            </div>
        </div>
        <div class="field">
            <label class="label">Författare</label>
            <div class="control">
                <input v-model="author" class="input" type="text" placeholder="">
            </div>
        </div>
        <div class="field">
            <label class="label">Förlag</label>
            <div class="control">
                <input v-model="publisher" class="input" type="text" placeholder="">
            </div>
        </div>
        <div class="field">
            <label class="label">År</label>
            <div class="control">
                <input v-model="year" class="input" type="number" placeholder="">
            </div>
        </div>
        <label class="label">Har du läst boken?</label>
        <div class="control">
            <div class="select">
                <select v-model="read" name="read" id="read" form="form">
                    <option v-bind:value=true >Ja</option>
                    <option v-bind:value=false >Nej</option>
                </select>
            </div>
        </div>
        <div class="mt-5"></div>
        <div class="field">
            <div class="control">
                <input class="button is-primary" type="submit" value="Lägg till">
            </div>
        </div>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                title: "",
                author: "",
                publisher: "",
                year: "",
                read: ""
            }
        },
        //emits
        emits: ["bookAdded"],
        //methods
        methods: {
            async addBook() {
                if(this.title.length > 4) {

                    let bookBody = {
                        title: this.title,
                        author: this.author,
                        publisher: this.publisher,
                        year: this.year,
                        read: this.read
                    };

                    const resp = await fetch("https://moment-2-beaabrahamsson.herokuapp.com/api/books", {
                        method:"POST",
                        headers: {
                        "Accept": "application/json",
                        "Content-type": "application/json"
                        },
                        body: JSON.stringify(bookBody)
                    });

                    const data = await resp.json();

                    this.title = "";
                    this.author = "";
                    this.publisher = "";
                    this.year = "";
                    this.read = "";

                    this.$emit("bookAdded");
                }
            }
        }
    }
</script>