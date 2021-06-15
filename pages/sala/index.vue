<template>
  <div>
    <div v-if="usuario.tipo == `admin`">
      <b-container>
        <b-row>
          <b-col cols="9">
            <h2>Salas</h2>
          </b-col>
          <b-col class="text-right">
            <b-button pill href="/sala/new" variant="primary"
              ><b-icon icon="clipboard-plus"></b-icon> Nova Sala</b-button
            >
          </b-col>
        </b-row>

        <br />

        <b-list-group>
          <div v-for="sala of salas" :key="sala.id">
            <b-list-group-item
              class="d-flex justify-content-between align-items-center"
            >
              {{ sala.nome }}
              <a href="#"
                ><b-icon
                  icon="trash"
                  variant="danger"
                  @click="remove(sala.id)"
                ></b-icon
              ></a>
            </b-list-group-item>
          </div>
        </b-list-group>
      </b-container>
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
      salas: [],
    };
  },
  computed: {
    usuario() {
      return this.$store.state.auth.user;
    },
  },
  async fetch() {
    const { data } = await this.$axios.get("sala");
    this.salas = data;
  },
  methods: {
    async remove(id) {
      console.log("remover");
      await this.$axios.delete(`sala/${id}`);
      const { data } = await this.$axios.get("sala");
      this.salas = data;
    },
  },
};
</script>

<style scoped>
#divisor {
  margin-top: 80px;
  margin-bottom: 50px;
}
</style>