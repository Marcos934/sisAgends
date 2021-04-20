<template>
  <div class="container is-max-desktop">
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
            <td>Ação</td>
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
export default {
  props: {
    dados: Object,
  },
  data() {
    return {
      index: null,
    };
  },
  methods: {},
};
</script>
<style scoped>
</style>