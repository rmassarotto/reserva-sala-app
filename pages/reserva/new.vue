<template>
  <div>
    <h1>Reserve sua Sala</h1>
    <p>Informe os dados abaixo para fazer uma reserva</p>

    <b-alert v-model="conflito" variant="danger" dismissible>
      Atenção! Já existe uma sala reservada entre os horarios definidos.
    </b-alert>

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
  middleware: "auth",
  data() {
    return {
      sala: null,
      data: null,
      inicio: "",
      fim: "",
      salas: [],
      conflito: false,
    };
  },
  async fetch() {
    const { data } = await this.$axios.get("sala");
    this.salas = data;
  },
  computed: {
    usuario() {
      return this.$store.state.auth.user;
    },
  },
  methods: {
    async verificaConflitoReserva(data, salaId, inicio, fim) {
      const result = await this.$axios.get(
        `reserva/${data}/${salaId}/${inicio}/${fim}`
      );
      return result.data;
    },
    async salvar() {
      if (
        await this.verificaConflitoReserva(
          this.data,
          this.sala,
          this.inicio,
          this.fim
        )
      ) {
        this.conflito = true;
      } else {
        let reserva = {
          usuarioId: this.usuario.id,
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
      }
    },
  },
};
</script>

