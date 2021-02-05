<template>
    <div>
        <h4 class="text-center mt-20">
            <small>
            <button class="btn btn-success" v-on:click="navigate()"> VER TODOS LOS AFILIADOS </button>
            </small>
        </h4>

        <div class="col-md-12 form-wrapper">
            <h2> Editar Afiliado </h2>

            <form id="create-post-form" @submit.prevent="editCustomer">


                <div class="form-group col-md-12">
                <label for="title"> DNI </label>
                <input type="text" id="DNI" v-model="customer.dni" name="title" class="form-control" placeholder="Ingresa DNI">
                </div>

                <div class="form-group col-md-12">
                <label for="title"> Nombre </label>
                <input type="text" id="nombre" v-model="customer.name" name="title" class="form-control" placeholder="Nombres">
                </div>

                <div class="form-group col-md-12">
                <label for="title"> Apellidos </label>
                <input type="text" id="apellidos" v-model="customer.last_name" name="title" class="form-control" placeholder="Apellidos">
                </div>

                <div class="form-group col-md-12">
                <label for="title"> Teléfono </label>
                <input type="text" id="telefono" v-model="customer.phone" name="title" class="form-control" placeholder="N° Teléfono">
                </div>                

                <div class="form-group col-md-12">
                <label for="title"> Email </label>
                <input type="text" id="mail" v-model="customer.mail" name="title" class="form-control" placeholder="Email">
                </div>

                <div class="form-group col-md-4 pull-right">
                    <button class="btn btn-success" type="submit"> Editar Afiliado </button>
                </div>      </form>
        </div>
    </div>   
</template>


<script>

import { server } from "../../helper";

import axios from "axios";

import router from "../../router";

export default {
    data() {
        return {
            id: 0,
            customer: {}
        };
    },

    created() {
        this.id = this.$route.params.id;
        this.getCustomer();
    },

    methods: {
        editCustomer() {
            let customerData = {
                DNI: this.customer.DNI,
                nombre: this.customer.nombre,
                apellidos: this.customer.apellidos,
                mail: this.customer.mail,
                telefono: this.customer.telefono
            };

            axios

                .put(
                    `${server.baseURL}/customer/update?customerID=${this.id}`,
                    customerData
                )
                /* exported variableName */
                .then(data => {

                    router.push({name: "home"});
                });
                
        },

        getCustomer() {
            axios
                .get(`${server.baseURL}/customer/customer/${this.id}`)
                .then(data => (this.customer = data.data));
        },

        navigate() {
            router.go(-1);
        }
    }
};
</script>