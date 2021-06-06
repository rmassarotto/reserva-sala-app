<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-md-12 d-flex vh-100 justify-content-center">
        <div class="col-md-4 align-self-center">
          <h1>Reserva</h1>
          <p>Informe os dados abaixo para acessar</p>

          <b-form @submit.prevent="loginUser">
            <b-form-group>
              <b-form-input
                v-model="login"
                placeholder="Login"
                required
              ></b-form-input>
            </b-form-group>

            <b-form-group>
              <b-form-input
                v-model="senha"
                type="password"
                placeholder="Senha"
                required
              ></b-form-input>
            </b-form-group>

            <b-button block type="submit" variant="primary">Acessar</b-button>
          </b-form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      login: null,
      senha: null,
    };
  },
  methods: {
    async loginUser() {
      try {
        await this.$auth.loginWith("local", {
          data: {
            loginUser: this.login,
            senha: this.senha,
          },
        });

        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>

