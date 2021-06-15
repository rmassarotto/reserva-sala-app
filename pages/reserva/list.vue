<template>
  <div>
    <b-container>
      <b-row>
        <b-col cols="9">
          <h2>Salas Reservadas</h2>
        </b-col>
        <b-col class="text-right">
          <b-button pill href="/reserva/new" variant="primary"
            ><b-icon icon="clipboard-plus"></b-icon> Nova Reserva</b-button
          >
        </b-col>
      </b-row>

      <br />

      <b-list-group>
        <div v-for="reserva of reservas" :key="reserva.id">
          <b-list-group-item
            class="d-flex justify-content-between align-items-center"
          >
            {{ reserva.id }} - {{ reserva.sala.nome }} | {{ reserva.inicio }} ->
            {{ reserva.fim }} | {{ reserva.data }} | {{ reserva.usuario.nome }}
            <a href="#"
              ><b-icon
                icon="trash"
                variant="danger"
                @click="remove(reserva.id)"
              ></b-icon
            ></a>
          </b-list-group-item>
        </div>
      </b-list-group>
    </b-container>
  </div>
</template>

<script>
export default {
  layout: "navbar",
  middleware: "auth",
  data() {
    return {
      reservas: [],
    };
  },
  async fetch() {
    const { data } = await this.$axios.get("reserva");
    this.reservas = data;
  },
  methods: {
    async remove(id) {
      console.log("remover");
      await this.$axios.delete(`reserva/${id}`);
      const { data } = await this.$axios.get("reserva");
      this.reservas = data;
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