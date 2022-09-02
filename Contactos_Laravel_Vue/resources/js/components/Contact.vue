<template>
    <div>
        <h1 class="text-center">Agenda de Contactos</h1>
        <hr>
        <table class="table">
            <thead class="table-dark">
                <tr>
                <th scope="col">Id</th>
                <th scope="col">Nombre</th>
                <th scope="col">Apellido</th>
                <th scope="col">Email</th>
                <th scope="col">Teléfono</th>
                <th scope="col">Dirección</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="contacto in contactazos" :key="contacto.id">
                <th scope="row">{{ contacto.id }}</th>
                <td>{{ contacto.nombre }}</td>
                <td>{{ contacto.apellido }}</td>
                <td>{{ contacto.email }}</td>
                <td>{{ contacto.tele }}</td>
                <td>{{ contacto.direccion }}</td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                contactazos: [], //no importa cómo bauticemos el array
            }
        },
        methods: {
            async listado() {
                const respuesta = await axios.get('contactos')  //un await solo puede ir dentro
                                                                //de un async
                this.contactazos = respuesta.data  //en todos los casos se debe poner .data a la respuesta para poder ver correctamente los datos
            }
        },
        created() {
            this.listado()    //con created() se carga la función o los datos tan pronto
                              //se inicializa la página sin oprimir ningún botón
        },
    }
</script>

<style>

</style>
