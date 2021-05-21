<template>
  <div>    
 <b-container class="mt-3">
     <h1 class="mb-5 mt-5 text-center">Lista de libros</h1>
  <b-row>
    <b-col cols="3"><h5>Nombre Libro:</h5></b-col>
    <b-col cols="3"><h5>Autor</h5></b-col>
    <b-col cols="2"><h5>Editorial</h5></b-col>
    <b-col cols="2"><h5>Fecha Edicion</h5></b-col>
    <b-col cols="1"><h5>Editar</h5></b-col>
    <b-col cols="1"><h5>Eliminar</h5></b-col>
  </b-row>
  <div class="divider div-transparent"></div>
  <br>
        <div v-bind:key="book.id" v-for="book in books">
            <BookItem v-bind:book="book" v-on:del-book-item="delBookMethod" v-on:edit-book-item="editBookMethod" />
        </div>
        <div v-if="!books.length">
            <p>No se encontraron libros guardados!!</p>
        </div>
        </b-container>
    </div>

</template>

<script>
    import BookItem from "./BookItem";
    export default {
        name: "Books",
        msg: 'SOY LUIS BRO',
        props: ["books"],
        components: {
            BookItem
        },
        methods: {
            delBookMethod(id){
               
                //send to parent
                this.$emit('del-book-event', id);
            },
            editBookMethod(id){
                //send to parent (App.vue)
                this.$emit('edit-book-event', id)
            }
        }
    }
</script>


<style>

</style>