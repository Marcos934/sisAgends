<template >
  <div class="container">
    <div class="notification is-white">
      <table id="tabela" class=" table display" style="width: 100%">
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
          <tr class="mt-5" v-for="dado in dados" :key="dado.id">
            <td>{{ dado.nome }}</td>
            <td>{{ dado.telefone }}</td>
            <td>{{ dado.email }}</td>
            <td>{{ dado.sexo }}</td>
            <td>
              <button
                @click="editar(dado)"
                class="button is-small is-warning mr-2"
              >
                <strong>Editar</strong>
              </button>
              <button @click="excluir(dado)" class="button is-small is-danger">
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
<div v-if="visivel">
  <Modal :editarDados="editarDados" @fecharComponente="modalEvento" @atualiza="atualizaRequest" />
</div>
</template>

<script>
const axios = require("axios");
import Modal from "@/components/Modal";
export default {
  components: {
    Modal,
  },
  props: {
    dados: Object,
  },
  data() {
    return {
      visivel: false,
      index: null,
      editarDados: '',

    };
  },
  methods: {
   async  excluir(valor) {
      if (
        !confirm("Deseja realemente excluir o contato de: " + valor.nome + " ?")
      ) {
        return 0;
      }
   await axios
        .delete("http://localhost:8080/api/deletar", {
          data: { id: valor.id },
        })

        .then((res) => {
          this.atualizaRequest();
          console.log(res.status);
        })
        .catch((err) => {
          console.log(err.response);
        });
        this.atualizaRequest()
    },
    editar(valor) {
      this.modalEvento()
      this.editarDados = valor
    },
    modalEvento(){
        this.visivel = !this.visivel;
    }
    ,
    atualizaRequest() {
      this.$emit("atualiza");
    },
  },
};
</script>
<style scoped>
</style>