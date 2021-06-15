<template>
  <div>
    <div v-if="usuario.tipo == `admin`">
      <h1>Cadastrar Sala</h1>
      <p>Informe os dados abaixo</p>

      <b-form @submit.prevent="salvar">
        <b-row>
          <b-col sm="10">
            <b-form-group>
              <label>Nome</label>
              <b-form-input
                v-model="nome"
                placeholder="Informe o nome da sala"
              ></b-form-input>
            </b-form-group>
          </b-col>
          <b-col>
            <label>&nbsp;</label>
            <b-button block type="submit" variant="primary">Salvar</b-button>
          </b-col>
        </b-row>
      </b-form>
    </div>
    <div v-else>
      <div class="text-center"><h2>Você não tem acesso a essa página!</h2></div>
    </div>
  </div>
</template>

<script>
export default {
  layout: "navbar",
  middleware: "auth",
  data() {
    return {
      nome: null,
    };
  },
  computed: {
    usuario() {
      return this.$store.state.auth.user;
    },
  },
  methods: {
    async salvar() {
      let self = this;
      await this.$axios
        .post("sala", { nome: this.nome })
        .then(function (response) {
          console.log(response);
          self.$router.push("/sala");
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>

