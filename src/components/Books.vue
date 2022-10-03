<template>
    <div class="columns">
            <div class="column">
                <div class="container">
                    <div class="mt-6"></div>
                    <!--book title -->
                    <h3 class="title is-4">
                    Bok med id {{title.id}}
                    </h3>
                    <div class="mb-3"></div>
                </div>
                <!-- table -->
                <div class="table-container">
                    <table class="table">
                        <thead>
                            <tr>
                                <th>Titel</th>
                                <th>Författare</th>
                                <th>Utgivare</th>
                                <th>År</th>
                                <th>Läst</th>
                                <th>Ta bort</th>
                            </tr>
                        </thead>
                        <tr>
                            <td>{{title.title}}</td>
                            <td>{{title.author}}</td>
                            <td>{{title.publisher}}</td>
                            <td>{{title.year}}</td>
                            <td v-if="title.read == 0">Nej</td>
                            <td v-if="title.read == 1">Ja</td>
                            <div class="level-item">
                                <td class="delete is-medium" @click="$emit('deleteBook')">Ta bort</td>
                            </div>
                        </tr>
                    </table>
                </div>
            </div>
    </div>
</template>

<script>
import { isIntegerKey } from '@vue/shared';

    export default {
        //props
        props: {
            title: String,
            author: String,
            publisher: String,
            year: Number,
            read: Boolean
        }
    }
</script>

<style scoped>
    .level-item {
        padding-top: 7px;
    }

</style>