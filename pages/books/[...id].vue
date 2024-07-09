<template>
<div v-if="error">
    <p>Error: {{ error }}</p>
</div>
<div v-else-if="book">
    <div class="mb-10">
        <div class="text-3xl font-bold">{{ book.title }}</div>
        <p class="text-lg  font-semibold" v-if="book.field_author_creator">{{ book.field_author_creator }}</p>
    </div>
    <!-- Flexboxes -->
    <div class="flex flex-col md:flex-row gap-5">

        <div class="md:w-1/2" >
            <p v-if="book.field_description">{{ book.field_description }}</p>
            <p v-if="book.field_abstract">{{ book.field_abstract }}</p>
            <div v-if="book.field_permalink">
                <NuxtLink to= {{book.field_permalink.value}} target="_blank">
                    <div class="buttonBack font-bold">
                     Click here for more data on this publication and availability on Limo
                    </div>
                </NuxtLink>
            </div>
        </div>

        <div class="md:w-1/2" >
            <hr>
            <p v-if="book.field_author_creator"><strong>Author:</strong> {{ book.field_author_creator }}</p>
            <p v-if="book.field_collaborator"><strong>Collaborators:</strong> {{ book.field_collaborator }}</p>
            <p v-if="book.field_editor"><strong>Editor:</strong> {{ book.field_editor }}</p>
            <div>
                <p v-if="book.field_date_of_publication"><strong>Date of publication: </strong>{{ book.field_date_of_publication }}</p>
                <p v-if="book.field_language">Language of this publication: {{ book.field_language }}</p>
                <p v-if="book.field_number_of_pages">Number of pages: {{ book.field_number_of_pages }}</p>
            </div>
            <hr>
            <div class="text-sm mt-5">
                <p class="pb-3" v-if="book.field_other_titles"><strong>Other title:</strong> {{ book.field_other_titles }}</p>
                <p class="pb-3" v-if="book.field_extent_of_the_edition"><strong>Extend of the edition:</strong> {{ book.field_extent_of_the_edition }}</p>
                <p class="pb-3" v-if="book.field_isbn">{{ book.field_isbn }}</p>
                <div class="pb-3" v-if="book.field_genre_form">genre: <span class="data" v-html="book.field_genre_form"></span><br></div>
                <div class="pb-3" v-if="book.field_event">event: <span class="data" v-html="book.field_event"></span><br></div>
                <div class="pb-3" v-if="book.field_source">source: <span class="data" v-html="book.field_source"></span><br></div>
                <div class="pb-3" v-if="book.field_subjects">subjects: <span class="data" v-html="book.field_subjects"></span></div>
                <hr>
                <p class="text-sm"><strong>id number: </strong> {{ book.id }}</p>
            </div>
        </div>
    </div>
    <!-- end Flexboxes -->  
     
    <div class="buttonBack font-bold mt-10">
        <NuxtLink to="/books">Back to the full list of books</NuxtLink>
    </div>    
</div>
<div v-else>
    <p>Loading...</p>
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const book = ref(null);
const error = ref(null);

onMounted(async () => {
const bookId = parseInt(route.params.id);

try {
    const response = await fetch('/data/books.json');
    if (!response.ok) {
    throw new Error('Failed to fetch books data');
    }
    const data = await response.json();
    let found = false;
    for (let b of data) {
    // console.log(b.id)
    // console.log(bookId)
    if (b.id == bookId) {
        book.value = b;
        found = true;
        break;
    }
    }
    if (!found) {
    error.value = `Book with ID ${bookId} not found.`;
    }
} catch (err) {
    error.value = `Error fetching data: ${err.message}`;
    console.error('Error fetching data:', err);
}
});
</script>

<style>
.buttonBack{
    border: 1px solid #ccc;
    border-radius: .2em;
    margin-top: 1em;
    padding: .75em;
    width:max-content;
    max-width: 40vw;
}
</style>