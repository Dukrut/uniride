<template>
  <div class="q-pa-lg">
    <q-btn @click="onNewUser()">Novo usuário</q-btn>
    <q-table
      v-if="list_user.length >= 1 ? true : false"
      title="Lista de usuários"
      :rows="list_user"
      class="table-uniride"
      :columns="columns"
      row-key="name"
      binary-state-sort
      rows-per-page-label="Registros por página"
      @row-click="onRowSelected"
    >
    </q-table>

    <q-dialog v-model="showModalEdit" full-width>
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
            <q-input
              v-model="user.fullname"
              :error="error.fullname"
              label="Nome completo"
              @update:modelValue="clearError('fullname')"
            ></q-input>
          </div>
          <div class="col-6 q-px-lg">
            <q-input
              v-model="user.mail"
              label="E-mail"
              :error="error.mail"
              @update:modelValue="clearError('mail')"
            ></q-input>
          </div>
        </div>

        <div class="row q-mt-md">
          <div class="col-3 q-px-lg">
            <q-input
              :error="error.cpf"
              v-model="user.cpf"
              mask="###.###.###-##"
              label="CPF"
              @update:modelValue="clearError('cpf')"
            ></q-input>
          </div>
          <div class="col-3 q-px-lg">
            <q-input
              :error="error.password"
              v-model="user.password"
              type="password"
              label="Senha"
              @update:modelValue="clearError('password')"
            ></q-input>
          </div>
          <div class="col-3 q-px-lg">
            <q-select
              label="Gênero"
              :error="error.gender"
              v-model="user.gender"
              @update:modelValue="clearError('gender')"
              emit-value
              map-options
              :options="[
                { label: 'Masculino', value: 'male' },
                { label: 'Feminino', value: 'female' },
                { label: 'Outro', value: 'other' },
              ]"
            ></q-select>
          </div>
          <div class="col-3 q-px-lg">
            <q-input
              :error="error.age"
              v-model="user.age"
              mask="###"
              label="Idade"
              @update:modelValue="clearError('age')"
            ></q-input>
          </div>
        </div>
        <div class="col-12 q-px-lg q-mt-lg">
          <q-btn @click="onSave()" class="text-green-8">Salvar</q-btn>
          <q-btn @click="onDelete()" class="q-ml-sm text-red-8">Deletar</q-btn>
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
      is_edit: true,
      list_user: [],
      user: {
        fullname: null,
        mail: null,
        age: null,
        gender: null,
        cpf: null,
        password: null,
      },
      showModalEdit: false,
      error: {
        fullname: false,
        mail: false,
        age: false,
        gender: false,
        cpf: false,
        password: false,
      },
      columns: [
        {},
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

  setup() {
    const $q = useQuasar();

    return {
      showNotify(type, message) {
        $q.notify({
          type: type,
          position: "top-right",
          message: message,
          timeout: 3000,
        });
      },

      showLoading(message) {
        $q.loading.show({
          message: message,
          spinnerColor: "orange",
          spinnerSize: 140,
          backgroundColor: "green",
          messageColor: "black",
        });

        // hiding in 3s
        let timer = setTimeout(() => {
          $q.loading.hide();
          timer = void 0;
        }, 3000);
      },
    };
  },

  mounted() {
    this.getListUsers();
  },

  watch: {
    showModalEdit() {
      if (this.showModalEdit == false) this.user = {};
      this.clearError();
    },
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
          if (response.data) this.list_user = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    getUser(id) {
      axios({
        method: "GET",
        url: "http://localhost:8081/users?id=" + id,
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      })
        .then((response) => {
          if (response.data) this.user = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },

    onRowSelected(evt, row, index) {
      this.showModalEdit = true;
      this.is_edit = true;
      this.getUser(row.id);
    },

    onDelete() {
      axios({
        method: "DELETE",
        url: "http://localhost:8081/users?id=" + this.user.id,
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
        data: this.user,
      })
        .then((response) => {
          if (response.data == "success") {
            this.showNotify("positive", "O usuário foi deletado com sucesso.");

            this.showModalEdit = false;
            this.user = {};
          } else {
            this.showNotify(
              "negative",
              "Ocorreu uma falha ao deletar o usuário."
            );
          }
        })
        .catch((error) => {
          this.showNotify(
            "negative",
            "Ocorreu uma falha ao deletar o usuário."
          );
        })
        .finally(() => {
          this.getListUsers();
        });
    },

    onSave() {
      if (this.validateForm()) {
        this.showNotify("negative", "Preencha todos os campos");
        return;
      }

      axios({
        method: this.is_edit ? "PUT" : "POST",
        url: this.is_edit
          ? "http://localhost:8081/users?id=" + id
          : "http://localhost:8081/users",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
        data: this.user,
      })
        .then((response) => {
          if (response.data == "success") {
            this.showNotify(
              "positive",
              "O usuário foi atualizado com sucesso."
            );

            this.showModalEdit = false;
            this.user = {};
          } else {
            this.showNotify(
              "negative",
              "Ocorreu uma falha ao atualizar o usuário."
            );
          }
        })
        .catch((error) => {
          this.showNotify(
            "negative",
            "Ocorreu uma falha ao atualizar o usuário."
          );
        })
        .finally(() => {
          this.getListUsers();
        });
    },

    onNewUser() {
      this.showModalEdit = true;
      this.is_edit = false;
    },

    clearError(key = "") {
      if (key.length) {
        this.error[key] = false;
        return;
      }

      this.error.fullname = false;
      this.error.cpf = false;
      this.error.mail = false;
      this.error.password = false;
      this.error.age = false;
      this.error.gender = false;
    },

    validateForm() {
      if ([null, undefined, ""].includes(this.user.fullname))
        this.error.fullname = true;

      if ([null, undefined, ""].includes(this.user.password))
        this.error.password = true;

      if ([null, undefined, ""].includes(this.user.mail))
        this.error.mail = true;

      if ([null, undefined, ""].includes(this.user.cpf)) this.error.cpf = true;

      if ([null, undefined, ""].includes(this.user.age)) this.error.age = true;

      if ([null, undefined, ""].includes(this.user.gender))
        this.error.gender = true;

      let has_error =
        this.error.password ||
        this.error.fullname ||
        this.error.cpf ||
        this.error.mail ||
        this.error.gender;

      return has_error;
    },
  },
};
</script>

<style>
.table-uniride {
  height: 80vh;
  margin-top: 10px;
}
</style>
