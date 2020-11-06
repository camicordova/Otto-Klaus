<template>
<div class="juguete">
    <form class="jumbotron col-6 mx-auto mt-4" @submit.prevent="onFormSubmit">
        <div class="form-group">
            <label for="exampleInputEmail1">Código</label>
            <input type="text" v-model="juguete.codigo" v-bind:class="{'form-control':true,'disabled':$route.params.id}">
        </div>
        <div class="form-group">
            <label for="exampleInputEmail1">Nombre</label>
            <input type="text" v-model="juguete.nombre" class="form-control">

        </div>
        <div class="form-group">
            <label for="exampleInputEmail1">Stock</label>
            <input type="number" v-model="juguete.stock" class="form-control">
        </div>
        <div class="form-group">
            <label for="exampleInputEmail1">Precio</label>
            <input type="number" v-model="juguete.precio" class="form-control">
        </div>
        <button type="submit" class="btn btn-primary" v-if="!$route.params.id">Agregar juguete</button>
        <button type="submit" class="btn btn-primary" v-if="$route.params.id">Editar juguete</button>
    </form>
</div>
</template>

<script>
import {
    db
} from '@/db'

export default {
    name: 'Juguete',
    components: {

    },
    data() {
        return {
            juguete: {
                codigo: "",
                nombre: "",
                stock: 0,
                precio: 0
            },
        }
    },
    mounted() {
        var that = this;
        if (that.$route.params.id) {
            db.collection('juguetes').doc(that.$route.params.id).get().then((juguete) => {
                that.juguete = juguete.data();
            })
        }
    },
    methods: {
        onFormSubmit(event) {
            var that = this;
            if (that.$route.params.id) {
                //editar
                var r = confirm('¿Seguro que desea editar este juguete?');
                if (r) {

                    db.collection('juguetes').doc(that.juguete.codigo).set(that.juguete).then((result) => {
                        console.log(result)
                        alert('Juguete editado')
                    }).catch((err) => {
                        console.log(err)
                    })
                }
            } else {
                //crear
                var r = confirm('¿Seguro que desea crear este juguete?');
                if (r) {

                    db.collection('juguetes').doc(that.juguete.codigo).set(that.juguete).then((result) => {
                        console.log(result)
                        alert('Juguete agregado')
                    }).catch((err) => {
                        console.log(err)
                    })
                }
            }
        }
    }
}
</script>

<style lang="scss">
.disabled {
    pointer-events: none;
    opacity: 0.5;
}
</style>
