<template>
    <div class="container">
        <div class="mt-6"></div>
        <!-- page title -->
        <h2 class="title is-2">Böcker</h2>
        <!-- form to add book -->
        <AddBook @bookAdded="getBooks()"/>
        <div class="mt-6"></div>
        <!-- list of books -->
        <h3 class="title is-3">Lista med böcker</h3>
        <Books @deleteBook="deleteBook(title.id)" v-for="title in books" :title="title" :key="title.id" />
    </div>
</template>

<script>
    import Books from "../components/Books.vue"
    import AddBook from "../components/AddBook.vue"

    export default {
        data() {
            return {
                books: []
            }
        },
        //components
        components: {
            Books,
            AddBook
        },
        //methods
        methods: {
            async getBooks() {
                const resp = await fetch("https://moment-2-beaabrahamsson.herokuapp.com/api/books");

                const data = await resp.json();

                this.books = data;
            },
            async deleteBook(id) {
                const resp = await fetch("https://moment-2-beaabrahamsson.herokuapp.com/api/books/" + id, {
                    method: "DELETE",
                    headers: {
                        "Accept": "application/json",
                        "Content-type": "application/json"
                    }
                });

                const data = await resp.json();

                this.getBooks();
            }
        },
        mounted() {
            this.getBooks();
        }
    }
</script>

<style scoped>
    h2 {
        text-align: center;
        font-size: 2em;
    }

    .container {
        margin: 100px;
    }
</style>