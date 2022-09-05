<template>
    <div>
        <h1 class="text-center">Agenda de Contactos</h1>
        <hr>
        <!-- Added Button trigger modal -->
        <button @click="update=false; openModal()" type="button" class="btn btn-primary">
        Nuevo contacto
        </button>

        <!-- Modal -->
        <!--originalmente estaba esta línea pero se borra buena parte de ella-->
        <!--<div class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">-->
        <div class="modal" :class="{mostrar:modal}"> <!--Esto es una clase dinámica. De hecho, mostrar es una clase
                                            que creamos en la sección style. Solo se activará si el atributo modal es true, es decir, 1-->
            <div class="modal-dialog">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">{{tituloModal}}</h5>
                    <button @click="closeModal()" type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    ...
                </div>
                <div class="modal-footer">
                    <button @click="closeModal()" type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
                    <button type="button" class="btn btn-success">Guardar cambios</button>
                </div>
                </div>
            </div>
        </div> <!--fin del div modal-->
        <br>
        <br>
        <table class="table table-striped table-hover">
            <thead class="table-dark">
                <tr>
                <th scope="col">Id</th>
                <th scope="col">Nombre</th>
                <th scope="col">Apellido</th>
                <th scope="col">Email</th>
                <th scope="col">Teléfono</th>
                <th scope="col">Dirección</th>
                <th scope="col" colspan="2" class="text-center">Acción</th>
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
                <td>
                    <button @click="update=true; openModal(contacto.id)" class="btn btn-warning">Editar</button>
                </td>
                <td>
                    <button @click="eliminar(contacto.id)" class="btn btn-danger">Eliminar</button>
                </td>
                </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                update:true,
                modal: 0, /*si el modal está cerrado será 0 y si está abierto será 1.Por default
                           lo inicializamos en 0 que significa false */
                tituloModal: '',
                contactazos: [], //no importa cómo bauticemos el array
            }
        },
        methods: {
            async listar() {
                const respuesta = await axios.get('contactos')  //un await solo puede ir dentro
                                                                //de un async
                this.contactazos = respuesta.data  //en todos los casos se debe poner .data a la respuesta para poder ver correctamente los datos
            },
            async eliminar(id) {
                const respuesta = await axios.delete('/contactos/' + id)  //un await solo puede ir dentro
                                                                //de un async
                this.listar() //con esto no tendremos que estar actualizando el navegador
            },
            openModal(id=0) {
                this.modal = 1
                if(this.update){
                    this.tituloModal = "Modificar contacto"
                }else{
                    this.tituloModal = "Crear contacto"
                }
            },

            closeModal(){
                this.modal = 0
            }

        },
        created() {
            this.listar()    //con created() se carga la función o los datos tan pronto
                              //se inicializa la página sin oprimir ningún botón
        },
    }
</script>

<style>
    .mostrar{ /*Solo se activará si modal es 1 (true) */
        display: list-item;
        opacity: 1;
        background: rgba(44, 38, 75, 0.849);
    }
</style>
