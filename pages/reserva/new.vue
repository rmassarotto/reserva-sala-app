<template>
  <div>
    <h1>Reserve sua Sala</h1>
    <p>Informe os dados abaixo para fazer uma reserva</p>

    <b-form @submit.prevent="salvar">
      <b-form-group>
        <label>Sala</label>
        <b-form-select
          v-model="sala"
          :options="salas"
          value-field="id"
          text-field="nome"
        >
          <b-form-select-option value="null">Selecione</b-form-select-option>
        </b-form-select>
      </b-form-group>
      <b-row>
        <b-col>
          <b-form-group>
            <label>Data</label>
            <b-form-datepicker
              id="dataReserva"
              v-model="data"
              class="mb-2"
              placeholder="Selecione a data"
            ></b-form-datepicker>
          </b-form-group>
        </b-col>
        <b-col>
          <b-form-group>
            <label>Inicio</label>
            <b-form-timepicker v-model="inicio"></b-form-timepicker>
          </b-form-group>
        </b-col>
        <b-col>
          <b-form-group>
            <label>Termino</label>
            <b-form-timepicker v-model="fim"></b-form-timepicker>
          </b-form-group>
        </b-col>
      </b-row>

      <b-button block type="submit" variant="primary">Salvar</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  layout: "navbar",
  data() {
    return {
      usuario: 1,
      sala: null,
      data: null,
      inicio: "",
      fim: "",
      salas: [],
    };
  },
  async fetch() {
    const { data } = await this.$axios.get("sala");
    this.salas = data;
  },
  methods: {
    async salvar() {
      let reserva = {
        usuarioId: this.usuario,
        salaId: this.sala,
        data: this.data,
        inicio: this.inicio,
        fim: this.fim,
      };
      let self = this;
      await this.$axios
        .post("reserva", reserva)
        .then(function (response) {
          console.log(response);
          self.$router.push("/reserva/list");
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
};
</script>

