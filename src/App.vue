<template>
  <Layout>
    <ModalAddContato @atualiza="atualiza" />
    <Agenda :dados="dados"  />
  </Layout>
</template>

<script>
import Layout from "@/layouts/Layout";
import Agenda from "@/components/Agenda";
import ModalAddContato from "@/components/ModalAddContato";
const axios = require("axios");
export default {
  components: {
    Layout,
    Agenda,
    ModalAddContato,
  },
  data() {
    return {
      dados: "",
    };
  },
  methods: {
    atualiza() {
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
