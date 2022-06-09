<template>
  <div class="q-pa-lg">
    <q-table
      v-if="list_user.length >= 1 ? true : false"
      title="Lista de usuários"
      :rows="list_user"
      :columns="columns"
      row-key="name"
      binary-state-sort
      rows-per-page-label="Registros por página"
      @row-click="onRowSelected(evt, row, index)"
      selection
      @selection="onRowSelected"
    >
    </q-table>

    <q-dialog v-model="fullHeight" style="width: 1000px">
      <q-card class="q-pa-lg">
        Dados do usuário
        <hr class="q-mb-md" />
        <div class="col-12">
          <q-avatar size="100px" class="q-px-lg">
            <img src="../assets/avatar.png" />
          </q-avatar>
        </div>
        <div class="row q-mt-md">
          <div class="col-6 q-px-lg">
            <q-input label="Nome completo"></q-input>
          </div>
        </div>

        <div class="row q-mt-md">
          <div class="col-6 q-px-lg">
            <q-input label="E-mail"></q-input>
          </div>
          <div class="col-46q-px-lg">
            <q-input label="CPF"></q-input>
          </div>
        </div>
        <div class="col-2 q-px-lg">
          <q-input label="Senha"></q-input>
          <small>*Insira somente se deseja alterar</small>
        </div>

        <div class="row q-mt-md">
          <div class="col-6 q-px-lg">
            <q-select
              label="Gênero"
              emit-value
              map-options
              :options="[
                { label: 'Masculino', value: 'male' },
                { label: 'Feminino', value: 'female' },
                { label: 'Outro', value: 'other' },
              ]"
            ></q-select>
          </div>
          <div class="col-1 q-px-lg">
            <q-input type="number" label="Idade"></q-input>
          </div>
        </div>
        <div class="col-12 justify-end q-px-lg q-mt-lg">
          <q-btn>Salvar</q-btn>
        </div>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import axios from "axios";
import { useQuasar } from "quasar";

export default {
  data() {
    return {
      list_user: [],
      fullHeight: false,
      columns: [
        {
          name: "fullname",
          required: true,
          label: "Nome completo",
          align: "left",
          field: (row) => row.fullname,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "email",
          required: true,
          label: "E-mail",
          align: "left",
          field: (row) => row.mail,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "cpf",
          required: true,
          label: "CPF",
          align: "left",
          field: (row) => row.cpf,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "age",
          required: true,
          label: "Idade",
          align: "left",
          field: (row) => row.age,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "is_driver",
          required: true,
          label: "É motorista",
          align: "left",
          field: (row) => row.is_driver,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "quantity_cars",
          required: true,
          label: "Quantidade carros",
          align: "left",
          field: (row) => row.quantity_cars,
          format: (val) => `${val}`,
          sortable: true,
        },
      ],
    };
  },

  mounted() {
    this.getListUsers();
  },

  methods: {
    getListUsers() {
      axios({
        method: "GET",
        url: "http://localhost:8081/users/all",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      })
        .then((response) => {
          console.log(response);
          if (response.data) this.list_user = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    onRowSelected() {
      this.fullHeight = true;
      console.log("teste");
    },
  },
};
</script>

<style></style>
