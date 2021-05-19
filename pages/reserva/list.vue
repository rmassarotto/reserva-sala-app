<template>
  <div>
    <b-container>
      <div class="text-center">
        <b-button href="/reserva/new">Nova Reserva</b-button>
      </div>
      <hr id="divisor" />

      <h2>Salas Reservadas</h2>

      <br />

      <b-list-group>
        <div v-for="reserva of reservas" :key="reserva.id">
          <b-list-group-item
            class="d-flex justify-content-between align-items-center"
          >
            {{ reserva.salaId }} - {{ reserva.data }} | {{ reserva.inicio }} ->
            {{ reserva.fim }} | {{ reserva.usuarioId }}
          </b-list-group-item>
        </div>
      </b-list-group>
    </b-container>
  </div>
</template>

<script>
export default {
  layout: "navbar",
  data() {
    return {
      reservas: [],
    };
  },
  async fetch() {
    const { data } = await this.$axios.get("reserva");
    // console.log(data);
    this.reservas = data;
  },
};
</script>

<style scoped>
#divisor {
  margin-top: 80px;
  margin-bottom: 50px;
}
</style>