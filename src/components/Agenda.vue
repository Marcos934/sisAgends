<template>
  <div class="container">
    <div class="notification is-white">
      <table id="example" class="display" style="width: 100%">
        <thead>
          <tr>
            <th>Nome</th>
            <th>Telefone</th>
            <th>Email</th>
            <th>Sexo</th>
            <th>Ação</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="dado in dados" :key="dado.id">
            <td>{{ dado.nome }}</td>
            <td>{{ dado.telefone }}</td>
            <td>{{ dado.email }}</td>
            <td>{{ dado.sexo }}</td>
            <td>
              <button class="button is-small is-warning mr-2">
                <strong>Editar</strong>
              </button>
              <button
                @click="excluir(dado.id)"
                class="button is-small is-danger"
              >
                <strong>Excluir</strong>
              </button>
            </td>
          </tr>
        </tbody>

        <tfoot>
          <tr>
            <th>Nome</th>
            <th>Telefone</th>
            <th>Email</th>
            <th>Sexo</th>
            <th>Ação</th>
          </tr>
        </tfoot>
      </table>
    </div>
  </div>
</template>

<script>
const axios = require("axios");
export default {
  props: {
    dados: Object,
  },
  data() {
    return {
      index: null,
    };
  },
  methods: {
    excluir(valor) {
      axios
        .delete("http://localhost:8080/api/deletar", {
          data: { id: valor },
        })

        .then((res) => {
          this.atualizaRequest();
          console.log(res.status);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
    atualizaRequest() {
      this.$emit("atualiza");
    },
  },
};
</script>
<style scoped>
</style>