<template>
  <div>
    <b-container>
      <div class="text-center">
        <b-button href="/reserva/new">Nova Reserva</b-button>
      </div>
      <hr id="divisor" />

      <h2>Minhas Reservas</h2>

      <br />
      <b-list-group>
        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          Cras justo odio
          <b-badge variant="primary" pill>14</b-badge>
        </b-list-group-item>

        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          Dapibus ac facilisis in
          <b-badge variant="primary" pill>2</b-badge>
        </b-list-group-item>

        <b-list-group-item
          class="d-flex justify-content-between align-items-center"
        >
          Morbi leo risus
          <b-badge variant="primary" pill>1</b-badge>
        </b-list-group-item>
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