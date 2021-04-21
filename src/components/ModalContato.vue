<template>
  <nav>
    <div class="navbar-menu is-active">
      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            <a class="button is-success is-hovered is-fullwidth" @click="modal">
              <strong>Adicionar novo contato</strong>&nbsp;
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="24"
                height="24"
                viewBox="0 0 24 24"
              >
                <path
                  d="M12 0c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm3.445 17.827c-3.684 1.684-9.401-9.43-5.8-11.308l1.053-.519 1.746 3.409-1.042.513c-1.095.587 1.185 5.04 2.305 4.497l1.032-.505 1.76 3.397-1.054.516z"
                />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>
  </nav>
  <!-- is-active -->
  <!-- is-clipped -->
  <div v-if="visivel == true" class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-card">
      <header class="modal-card-head">
        <p class="modal-card-title">Adicionar novo contato</p>
        <button class="delete" @click="modal"></button>
      </header>

      <section class="modal-card-body">
        <div v-if="errors.length != []" class="message is-warning">
          <div class="message-header">
            Por favor, corrija o(s) seguinte(s) erro(s):
          </div>
          <div class="message-body">
            <ol>
              <li v-for="error in errors" :key="error">
                {{ error }}
              </li>
            </ol>
          </div>
        </div>
        <form @submit.prevent="submit">
          <label class="label">Nome</label>
          <input
            class="input is-link"
            type="text"
            v-model="form.nome"
            placeholder="Fulano de tal"
            required
            maxlength="85"
          />

          <label class="label mt-2">Telefone</label>
          <input
            @keyup="validarNumero"
            class="input telefone is-link"
            type="text"
            v-model="form.telefone"
            placeholder="991461245"
            pattern="\([0-9]{2}\) [0-9]{4,6}-[0-9]{3,4}$"
            maxlength="13"
            minlength="9"
            required
          />

          <label class="label mt-2">Email</label>
          <input
            class="input is-link"
            type="email"
            v-model="form.email"
            placeholder="exemplo@gmail.com"
            maxlength="85"
            required
          />

          <label class="label mt-3">Sexo</label>
          <div class="control">
            <div class="select">
              <select required v-model="form.sexo">
                <option selected disabled>Selecione</option>
                <option value="M">M - (Masculino)</option>
                <option value="F">F - (Feminino)</option>
              </select>
            </div>
          </div>
        </form>
      </section>
      <footer class="modal-card-foot">
        <button v-if="load" class="button is-success is-loading">Aguarde</button>
        <button
          v-else
          class="button is-success"
          @click="salvarContato"
        >
          Salvar Contato
        </button>
        <button class="button" @click="modal">Cancelar</button>
      </footer>
    </div>
    <div else class="modal is-clipped"></div>
  </div>
</template>
<script>
import "@/assets/js/bulma-events.js";

const axios = require("axios");
export default {
  data() {
    return {
      errors: [],
      visivel: false,
      load: false,
      form: {
        nome: "",
        sexo: "",
        telefone: "",
        email: "",
      },
    };
  },
  methods: {
    modal() {
      this.visivel = !this.visivel;
    },
   async salvarContato() {
     this.load = true
      this.errors = [];
      if (this.checkForm()) {
        alert("Preencha todos os campos corretamente");
      } else {
       await axios
          .post("http://localhost:8080/api/novo", this.form)
          .then((res) => {
            this.limpaValores();
            this.atualizaRequest();
            this.modal();
            this.errors = [];
            console.log(res.status);
          })
          .catch((err) => {
           alert(err);
          });
      }
       this.load = false
    },
    atualizaRequest() {
      this.$emit("atualiza");
    },
    limpaValores() {
      (this.form.nome = ""),
        (this.form.email = ""),
        (this.form.sexo = ""),
        (this.form.telefone = "");
    },
    checkForm() {
      let erro = false;
      if (!this.form.nome) {
        this.errors.push("O campo Nome é obrigatório.");
        erro = true;
      }
      if (!this.form.telefone) {
        this.errors.push("O campo Telefone é obrigatório.");
        erro = true;
      }
      if (!this.form.email) {
        this.errors.push("O campo Email é obrigatório.");
        erro = true;
      }
      if (!this.validEmail(this.form.email)) {
        this.errors.push("Email inválido, siga o formato: exemplo@gmail.com");
        erro = true;
      }
      if (!this.form.sexo) {
        this.errors.push("Escolha o sexo.");
        erro = true;
      }

      if (erro) {
        return true;
      } else {
        return false;
      }
    },
    validEmail(email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    validarNumero() {
      if (!Number(this.form.telefone) && this.form.telefone != "") {
        this.form.telefone = "";
        alert("Digite somente os números");
      }
    },
  },
};
</script>