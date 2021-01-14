<template>
  <div class="container-fluid">
    <div class="text-center">
      <h1>Aplicación de Gestión de Afiliados</h1>
    <p> Construido con Nest.js, Vue.js y MongoDB</p>

    <div v-if="customers.length === 0">
      <h2> No hay afiliados todavía (: </h2>
    </div>

  </div>

  <div class="">
    <table class="table table-bordered">
      <thead class="thead-dark">
        <tr>
          <th scope="col">DNI</th>
          <th scope="col">Nombre</th>
          <th scope="col">Apellidos</th>
          <th scope="col">Mail</th>
          <th scope="col">Teléfono</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="customer in customers" :key="customer._id">
          <td>{{ customer.DNI }}</td>
          <td>{{ customer.nombre }}</td>
          <td>{{ customer.appellidos }}</td>
          <td>{{ customer.mail }}</td>
          <td>{{ customer.telefono }}</td>
          <td>

            <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group" style="margin-bottom: 20px;">

                <router-link :to="{name: 'Edit', params: {id: customer._id}}" class ="btn btn-sm btn-outline-secondary"> Editar Afiliado </router-link>       

                 <button class="btn btn-sm btn-outline-secondary" v-on:click="deleteCustomer(customer._id)">Eliminar Afiliado</button>

                </div>

            </div>

          </td>
        </tr>
      </tbody>
    </table>
  </div>

  </div>
  


</template>


<script>
// @ is an alias to /src
import { server } from "../helper";

import axios from "axios";


export default {
  data() {
    return {
      customers: []
    };
  },
  created() {
    this.fetchCustomers();
  },
  methods: {
    fetchCustomers() {
      axios
        .get(`${server.baseURL}/customer/customers`)
        .then(data => (this.customers = data.data));
    },
    deleteCustomer(id) {
      axios
        .delete(`${server.baseURL}/customer/delete?customerID=${id}`)
        .then(data => {
          console.log(data);
          window.location.reload();
        });
    }
  }
};
</script>
