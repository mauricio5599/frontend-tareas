<template>
    <div>
        <h1 class="display-4 text-center">Listado de Tareas</h1>
        <hr>
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea" name="" id="" placeholder="Agregar Tarea"
                                class="form-control form-control-lg">
                            <div class="input-group-append">
                                <button v-on:click="agregarTarea()" type="text"
                                    class="btn btn-success btn-lg">Agregar</button>
                            </div>
                        </div>
                        <br>
                        <h5 v-if="listTareas.length == 0">No hay tareas para realizar</h5>
                        <ul class="list-group">
                            <template v-for="(tarea, index) of  listTareas " :v-key="index">
                                <li class="list-group-item d-flex justify-content-between">
                                    <span v-on:click="editarTarea(tarea, index)"
                                        v-bind:class="{ 'text-success': tarea.estado }" class="cursor">
                                        <i v-if="tarea.estado == false" class="fa-circle fa-regular"></i>
                                        <i v-else-if="tarea.estado == true" class="fa-solid fa-circle-check"></i>
                                    </span>
                                    {{ tarea.nombre }}
                                    <span v-on:click="eliminarTarea(index)" class="text-danger cursor">
                                        <i class="fa-solid fa-trash"></i>
                                    </span>
                                </li>
                            </template>

                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Tarea',
    data() {
        return {
            tarea: '',
            listTareas: []
        }
    },
    methods: {
        agregarTarea() {
            const tarea = {
                nombre: this.tarea,
                estado: false
            }
            this.listTareas.push(tarea);
            this.tarea = "";
        },
        eliminarTarea(index) {
            this.listTareas.splice(index, 1)
        },
        editarTarea(tarea, index) {
            this.listTareas[index].estado = !tarea.estado;
        }
    }
}
</script>

<style >
.cursor {
    cursor: pointer;
}
</style>
