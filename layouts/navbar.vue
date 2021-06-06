<template>
  <div>
    <b-navbar type="dark" variant="dark">
      <b-navbar-brand href="/">RESERVA</b-navbar-brand>
      <b-navbar-toggle target="notesBar"></b-navbar-toggle>

      <b-collapse id="notesBar" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-nav-item class="mr-3" href="/reserva/list">Reservasgit</b-nav-item>
          <b-nav-item-dropdown :text="primeiroNome" right>
            <b-dropdown-item href="#" @click.prevent="logout"
              >Sair</b-dropdown-item
            >
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <div class="container">
      <Nuxt />
    </div>
    <br />
  </div>
</template>

<script>
export default {
  computed: {
    usuario() {
      return this.$store.state.auth.user;
    },
    primeiroNome() {
      if (this.usuario) {
        const [nome] = this.usuario.nome.split(" ");
        return nome;
      }
    },
  },
  methods: {
    async logout() {
      await this.$auth.logout();
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped>
.navbar {
  margin-bottom: 80px;
}
</style>