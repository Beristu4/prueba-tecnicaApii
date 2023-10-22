<template>
  <div class="bg-success py-4">
    <div class="container">
      <div class="row">
        <div class="col-8">
          <input v-model="contractId" class="form-control" placeholder="Ingrese ID de contrato" type="text" />
        </div>
        <div class="col-4">
          <button @click="mounted" class="btn btn-outline-light w-100">Buscar</button>
        </div>
      </div>
    </div>
    <div class="container mt-4">
      <div v-if="contract">
        <h2 class="text-white">Detalles del Contrato</h2>
        <p><strong>Código de curso: </strong> {{ contract.codigoCurso }}</p>
        <p><strong>Fecha de alta: </strong> {{ contract.fechaAlta }}</p>
        <p><strong>Colegio: </strong> {{ contract.colegio }}</p>
        <p><strong>Nivel: </strong> {{ contract.nivel }}</p>
        <p><strong>Curso: </strong> {{ contract.curso }}</p>
        <p><strong>Localidad: </strong> {{ contract.localidad }}</p>
        <h2 class="text-white">Artículos del Pedido</h2>
        <table class="table">
          <thead>
            <tr>
              <th>Cantidad</th>
              <th>Artículo</th>
              <th>Precio unitario</th>
              <th>Total</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in contract.pedidos" :key="item.id">
              <td>{{ item.cantidad }}</td>
              <td>{{ item.articulo }}</td>
              <td>${{ item.precio }}</td>
              <td>${{ item.totalArticulo }}</td>
            </tr>
          </tbody>
        </table>
        <p><strong>Fecha de entrega: </strong> {{ contract.fechaEntrega }}</p>
        <h2 class="text-white"><strong>Total: </strong>${{ contract.montoPagar }}</h2>
      </div>
      <div v-else class="container-sm text-center">
        <img src="@/assets/6134065.png"  class="img-fluid w-30px h-30px" alt="Error" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      contractId: '',
      contract: null,
    };
  },
methods:{
    mounted () {
       axios
         .get(`https://localhost:7097/contrato/${this.contractId}`)
         .then(response => {
           this.contract = response.data
           console.log(response.data)
         })
         .catch(error => {
           console.log(error)
           this.contract = null;
         })
         .finally(() => this.loading = false)
     }
   }
};
</script>
