<template>
    <div class="container">

        <div class="card">
            <div class="card-header">
                Editar Contacto
            </div>
            <div class="card-body">

                <form v-on:submit.prevent="actualizarContacto" >
                    <div class="form-group">
                      <label for="nombres">Nombres:</label>
                        <input 
                            v-model="contacto.nombres"
                            type="text"
                            id="nombres"
                            class="form-control" 
                            name="nombres" 
                            placeholder="Nombres"
                            required
                        >
                    </div>

                    <div class="form-group">
                      <label for="apellidos">Apellidos:</label>
                        <input 
                            v-model="contacto.apellidos"
                            type="text"
                            id="apellidos"
                            class="form-control" 
                            name="apellidos" 
                            placeholder="Apellidos"
                            required
                        >
                    </div>

                    <div class="form-group">
                      <label for="correo">Correo:</label>
                        <input
                            v-model="contacto.correo" 
                            type="email"
                            id="correo"
                            class="form-control" 
                            name="correo" 
                            placeholder="Correo Electronico"
                            required
                        >
                    </div>

                    <div class="form-group">
                      <label for="telf_celular">Telefono Celular:</label>
                        <input
                            v-model="contacto.telefono_celular" 
                            type="text"
                            id="telf_celular"
                            class="form-control" 
                            name="telefono_celular" 
                            placeholder="Número de Telefono Celular"
                            required
                        >
                    </div>

                    <div class="form-group">
                      <label for="telf_habitacion">Telefono Habitación:</label>
                        <input
                            v-model="contacto.telefono_habitacion" 
                            type="text"
                            id="telf_habitacion"
                            class="form-control" 
                            name="telf_habitacion" 
                            placeholder="Número de Telefono Habitación"
                        >
                    </div>

                    <div class="float-right">
                        <div class="btn-group" role="group" aria-label="" style="align-text:center">
                            <router-link :to="{name:'Listar'}" class="btn btn-secondary">Cancelar</router-link>
                            <button type="submit" class="btn btn-primary">Guardar</button>
                        </div>
                    </div>

                </form>

            </div>
        </div>
       <br>
    </div>
</template>

<script>
import axios from 'axios';
export default {

    data(){
        return {
            contacto: {

            }
        }
    },
    created:function(){
        this.consultarInfoContacto()
    },

    methods:{
            
        consultarInfoContacto(){
            axios.get('http://localhost/api_phonebook/public/api/v1/contactos/'+this.$route.params.id)
            .then((datos) =>{
                this.contacto = datos.data
                console.log(datos.data)
            })
            .catch(console.log) 
        },

        actualizarContacto(){
            const qs = require('qs')
            var datosEnviar = {
                nombres : this.contacto.nombres,
                apellidos : this.contacto.apellidos,
                correo : this.contacto.correo,
                telefono_celular : this.contacto.telf_celular,
                telefono_habitacion : this.contacto.telf_habitacion
            }
            axios.put('http://localhost/api_phonebook/public/api/v1/contactos/update/'+this.$route.params.id,
                qs.stringify(datosEnviar)
            ).then(()=>{
                this.$swal({icon:"success", title: 'Contacto actualizado con éxito'})
                .then(function() {
                    window.location.href = '../listar'
                });
                

            })
        }
    }
}
</script>