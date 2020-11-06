<template>
<div class="home">
    <div class="jumbotron">
        <a class="btn btn-info btn-lg" href="/juguete">Agregar juguete</a>
    </div>
    <table class="table">
        <thead>
            <tr>
                <th scope="col">Código</th>
                <th scope="col">Nombre</th>
                <th scope="col">Stock</th>
                <th scope="col">Precio</th>
                <th scope="col">Acciones</th>

            </tr>
        </thead>
        <tbody>
            <tr v-for="(juguete,indice) in documents" v-bind:key="indice">
                <th scope="row">{{juguete.codigo}}</th>
                <td>{{juguete.nombre}}</td>
                <td>{{juguete.stock}}</td>
                <td>{{juguete.precio}}</td>
                <td>
                    <div class="btn-group" role="group" aria-label="Basic example">
                        <a class="btn btn-info" :href="'/juguete/'+juguete.codigo">Editar</a>
                        <button type="button" class="btn btn-danger" @click="borrarJuguete(juguete.codigo)">Eliminar</button>
                    </div>
                </td>
            </tr>
        </tbody>
    </table>
</div>
</template>

<script>
import {
    db
} from '@/db'

export default {
    name: 'Home',
    components: {

    },
    data() {
        return {
            documents: [],
        }
    },
    firestore: {
        documents: db.collection('juguetes'),
    },
    methods: {
        borrarJuguete(id) {
            var r = confirm('¿Está seguro que desea eliminar el juguete?');
            if (r) {
                db.collection('juguetes').doc(id).delete().then((result) => {
                    alert('Juguete eliminado')
                }).catch((err) => {
                    console.log(err)
                })
            }
        }
    }
}
</script>
