<template>

  <div>
    <b-container class="mb-2 mt-3">
    <b-row>
    <b-col cols="3">{{book.title}}</b-col>
    <b-col cols="3">{{book.autor}}</b-col>
    <b-col cols="2">{{book.editorial}}</b-col>
    <b-col cols="2">{{book.fechaEdicion}}</b-col>
    <b-col cols="1"><b-button variant="success" @click="$emit('edit-book-item', book.id)">Editar</b-button></b-col>
    <b-col cols="1"><b-button variant="danger" @click="$emit('del-book-item', book.id)">Eliminar</b-button></b-col>
  </b-row>
  <div class="divider div-transparent"></div>
  </b-container>
    </div>

</template>

<script>
    export default {
        name: "BookItem",
        props: ["book"]
    }
</script>


<style>
.divider
{
	position: relative;
	margin-top: 10px;
	height: 1px;
}

.div-transparent:before
{
	content: "";
	position: absolute;
	top: 0;
	left: 5%;
	right: 5%;
	width: 90%;
	height: 1px;
	background-image: linear-gradient(to right, transparent, rgb(48,49,51), transparent);
}
</style>
