<template>
  <Layout>
    <template #botaoModalContato>
      <ModalContato @atualiza="atualizar" />
    </template>
    <template #tabelaAgenda>
      <Agenda :dados="dados" @atualiza="atualizar" />
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
    atualizar() {
      axios
        .get("http://localhost:8080/api/contatos", {})
        .then((res) => {
          this.dados = res.data;
          //  console.log(this.dados);
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
  },
  mounted() {
    this.atualizar();
  },
};
</script>

<style>
</style>
