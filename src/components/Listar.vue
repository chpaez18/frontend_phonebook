<template>
    <div class="container">
        <div class="card">
            <div class="card-header">
                
                <div class="float-left"><h5>Contactos</h5></div>
                <div class="float-right"><router-link to="/crear" class="btn btn-primary">Agregar</router-link></div>
                
            </div>
            <div class="card-body">

                <table class="table">
                    <thead>
                        <tr>
                            <th>#</th>
                            <th>Nombre Completo</th>
                            <th>Correo</th>
                            <th>Telefono Celular</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>

                        <tr v-for="contacto in contactos" :key="contacto.id">
                            <td> {{contacto.id}} </td>
                            <td> {{contacto.nombres}} {{contacto.apellidos}} </td>
                            <td> {{contacto.correo}} </td>
                            <td> {{contacto.telefono_celular}} </td>
                            <td>
                                <div class="btn-group" role="group" aria-label="">
                                    <router-link :to="{name:'Editar', params:{id:contacto.id}}" class="btn btn-primary">Editar</router-link>
                                    <button type="button" v-on:click="eliminarContacto(contacto.id)" class="btn btn-danger">Borrar</button>
                                </div>
                            </td>
                        </tr>

                    </tbody>
                </table>

            </div>

        </div>    
    </div>


</template>

<script>
import axios from 'axios';
export default {
    
    data(){

        return {
            contactos: []
        }
    },

    created:function(){

        this.consultarContactos();

    },

    methods:{

        //Retorna el listado de contactos
        consultarContactos(){
            axios.get('http://localhost/api_phonebook/public/api/v1/contactos')
            .then((datos) =>{
                this.contactos = []
                if(datos.status == 200){
                    this.contactos = datos.data;
                }
            })
            .catch(console.log) 
        },

        //elimina un contacto 
        eliminarContacto(id){
            axios.delete('http://localhost/api_phonebook/public/api/v1/contactos/delete/'+id)
            .then(() =>{
                //console.log(datos)
                this.$swal({icon:"success", title: 'Contacto eliminado'})
                .then(function() {
                    window.location.href = 'listar'
                });
            })
            .catch(console.log) 
        }

    }
}
</script>