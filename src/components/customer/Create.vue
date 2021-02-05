<template>
    <div>
        <div class="col-md-12 form-wrapper">
            <h2> Crear Nuevo Afiliado </h2>
            <form id="create-post-form" @submit.prevent="createCustomer">

                <!-- DNI -->
                <div class="form-group col-md-12">
                    <label for="title"> DNI </label>
                    <input type="text" id="DNI" v-model="DNI" name="title" class="form-control" placeholder="Ingresa DNI">
                </div>

                <!-- Nombre -->
                <div class="form-group col-md-12">
                    <label for="title"> Nombre </label>
                    <input type="text" id="nombre" v-model="nombre" name="title" class="form-control" placeholder="Nombres">
                </div>                

                <!-- Apellidos  -->
                <div class="form-group col-md-12">
                    <label for="title"> Apellidos </label>
                    <input type="text" id="apellidos" v-model="apellidos" name="title" class="form-control" placeholder="Apellidos">
                </div>

                <!-- Mail -->
                <div class="form-group col-md-12">
                    <label for="title"> Email </label>
                    <input type="text" id="mail" v-model="mail" name="title" class="form-control" placeholder="Ingresa email">
                </div>

                <!-- Teléfono -->
                <div class="form-group col-md-12">
                    <label for="title"> Teléfono </label>
                    <input type="text" id="telefono" v-model="telefono" name="title" class="form-control" placeholder="N° Telefóno">                    
                </div>

                <div class="form-group col-md-4 pull-right">
                    <button class="btn btn-success" type="submit"> Añadir Afiliado</button>
                </div>      </form>    
        </div>
    </div>   
</template>

<script>

import axios from "axios";
import { server } from "../../helper";
import router from "../../router";

export default {
    data() {
        return {
            DNI: "",
            nombre: "",
            apellidos:"",
            mail: "",
            telefono:""
        };   
    },

    methods: {
        createCustomer() {
           // createCustomer() recibe los detalles del afiliado via el formulario 
            let customerData = {
                DNI: this.DNI,
                nombre: this.nombre,
                appellidos: this.apellidos,
                mail: this.mail,
                telefono: this.telefono
            };
            this.__submitToServer(customerData)
        },
        //AXIOS para mandar los datos de customerData al servidor.
        __submitToServer(data){
            /* exported variableName */
            axios.post(`${server.baseURL}/customer/create`, data).then(data => {
                router.push({ name: "home"});
            })
        }
    }
    
}
</script>
