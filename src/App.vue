<template>
  <Layout>
    <template #botaoModalContato>
      <ModalContato @atualiza="ref" />
    </template>
    <template #tabelaAgenda>
      <Agenda :dados="dados" @atualiza="ref" />
    </template>
  </Layout>
</template>

<script>
import Layout from "@/layouts/Layout";
import Agenda from "@/components/Agenda";
import ModalContato from "@/components/ModalContato";
const axios = require("axios");
export default {
  components: {
    Layout,
    Agenda,
    ModalContato,
  },
  data() {
    return {
      dados: null,
    };
  },
  methods: {
    async atualizar() {
      await axios
        .get("http://localhost:8080/api/contatos", {})
        .then((res) => {
          this.dados = res.data;
          //  console.log(this.dados);
        })
        .catch((err) => {
          alert(
            "Verifique se API minha agenda está em execução na porta 8080: " +
              err
          );
        });
     
    },
    ref(){
     location.reload();
    }
  },

  created() {
    this.atualizar();
  },
};
</script>

<style>
</style>
