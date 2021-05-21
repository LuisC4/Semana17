<template>
  <div class="text-center">
      <b-navbar type="dark" variant="dark">
          <b-navbar-nav>
              <b-container>
               <b-navbar-brand>Actividad Semana 17</b-navbar-brand>
              </b-container>
              </b-navbar-nav>
               <b-navbar-nav class="ml-auto">
                   <b-button variant="warning" href="https://github.com/LuisC4/Semana17" target="_blank">Respostorio</b-button>
                   </b-navbar-nav>

          </b-navbar>
      <b-jumbotron header="Registrar libros" lead="Registrar libro utilizando Vue.js, Local Storage">
  </b-jumbotron>
      <b-container>
          <h1>Registrar un nuevo libro</h1>
        <b-form inline @submit="addBook">
            <b-form-input
          v-model="title"
          type="text"
          placeholder="Titulo"
          class="mb-2 mr-sm-2 mb-sm-0"
        ></b-form-input>
        <b-form-input
          v-model="autor"
          type="text"
          placeholder="Autor"
          class="mb-2 mr-sm-2 mb-sm-0"
        ></b-form-input>
        <b-form-input
          v-model="editorial"
          type="text"
          placeholder="Editorial"
          class="mb-2 mr-sm-2 mb-sm-0"
        ></b-form-input>
        <b-form-datepicker 
        v-model="fechaEdicion" 
        placeholder="Fecha de edición"
        class="mb-2 mr-sm-2 mb-sm-0"></b-form-datepicker>
                <input type="submit" value="Agregar / Actualizar" class="btn btn-primary">
        </b-form>
        </b-container>
    </div>

</template>

<script>
    export default {
        name: "AddBookItem",
        props: ['editBook'],
        data () {
            return {
                title: '',
                autor: '',
                editorial: '',
                fechaEdicion: '',
                id: '',
                isbn:'',
                edit: false
            }
        },
        methods: {
            addBook(e){
                e.preventDefault();
                if (this.edit === false){
                    // add new book
                    const newBook = {
                        title: this.title,
                        autor: this.autor,
                        editorial: this.editorial,
                        fechaEdicion: this.fechaEdicion,
                        id: Math.floor(Math.random() * 100)
                    };
                    if (newBook.title !== ''){
                        this.$emit('add-book-event', newBook);
                    }
                    this.title = ''
                    this.editorial = '';
                    this.autor = '';
                    this.fechaEdicion = ''; 
                }else{
                    //edit book
                    const bookItem = {
                        title: this.title,
                        autor: this.autor,
                        editorial: this.editorial,
                        fechaEdicion: this.fechaEdicion,
                        id: this.id
                    };
                    //send to parent (App.vue)
                    this.$emit('edit-book-event', bookItem);
                    // clear input field
                    this.title = '';
                    this.editorial = '';
                    this.autor = '';
                    this.fechaEdicion = ''; 
                    this.edit = false;
                }
            }
        },
        watch: {
            editBook: {
                handler() {
                    this.autor = this.editBook.autor
                    this.editorial = this.editBook.editorial
                    this.fechaEdicion = this.editBook.fechaEdicion
                    this.title = this.editBook.title;
                    this.id = this.editBook.id;

                    this.edit = true
                },
                deep: true
            },
            title:{
                handler(){
                    if(this.title === '' || this.autor === '' || this.editorial === '' || this.fechaEdicion === ''){
                        this.edit = false;
                    }
                }
            }
        }
    }
</script>


<style>

</style>