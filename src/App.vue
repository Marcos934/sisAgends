<template>
  <Layout>
    <ModalContato @atualiza="atualizar" />
    <Agenda :dados="dados"  @atualiza="atualizar" />
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
      dados: "",
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
    axios
      .get("http://localhost:8080/api/contatos", {})
      .then((res) => {
        this.dados = res.data;
       // console.log(this.dados);
      })
      .catch((err) => {
        console.log(err.response);
      });
  },
};
</script>

<style>
</style>
