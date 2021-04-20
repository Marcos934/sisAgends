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
          <form @submit.prevent="submit">
            <label class="label">Nome</label>
            <input
              class="input is-link"
              type="text"
              v-model="form.nome"
              placeholder="Fulano de tal"
              required
            />

            <label class="label mt-2">Telefone</label>
            <input
              class="input is-link"
              type="number"
              v-model="form.telefone"
              placeholder="92912345678"
              required
            />

            <label class="label mt-2">Email</label>
            <input
              class="input is-link"
              type="email"
              v-model="form.email"
              placeholder="exemplo@gmail.com"
              required
            />

            <label class="label mt-3">Sexo</label>
            <div class="control">
              <div class="select">
                <select required v-model="form.sexo">
                  <option selected disabled>Selecione</option>
                  <option value="M">M - (Marculino)</option>
                  <option value="F">F - (Femenino)</option>
                </select>
              </div>
            </div>
          </form>
        </section>
        <footer class="modal-card-foot">
          <button class="button is-success" @click="salvarContato">
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
      visivel: false,
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
    salvarContato() {
      axios
        .post("http://localhost:8080/api/novo", this.form)
        .then((res) => {
        
        console.log(res.status)
            this.atualizaRequest()
            this.modal()
        })
        .catch((err) => {
          console.log(err.response);
        });
    },
    atualizaRequest(){
        this.$emit("atualiza")
    }
  },
};

</script>