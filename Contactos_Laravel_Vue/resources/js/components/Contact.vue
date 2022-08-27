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
                <tr v-for="contacto in contacts" :key="contacto.id">
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
                contacts: [],
            }
        },
        methods: {
            async listado() {
                const res = await axios.get('contactos')
                this.contacts = res.data
            }
        },
        created() {
            this.listado()
        },
    }
</script>

<style>

</style>
