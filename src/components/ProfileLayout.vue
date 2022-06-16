<template>
  <div class="full-width q-pa-lg">
    <q-card class="q-pa-lg">
      Meus dados
      <hr class="q-mb-md" />
      <div class="col-12">
        <q-avatar size="100px" class="q-px-lg">
          <img src="../assets/avatar.png" />
        </q-avatar>
      </div>
      <div class="row q-mt-md">
        <div class="col-6 q-px-lg">
          <q-input label="Nome completo" v-model="user_edit.fullname"></q-input>
        </div>
      </div>

      <div class="row q-mt-md">
        <div class="col-3 q-px-lg">
          <q-input label="E-mail" v-model="user_edit.mail"></q-input>
        </div>
        <div class="col-2 q-px-lg">
          <q-input label="CPF" v-model="user_edit.cpf"></q-input>
        </div>
        <div class="col-2 q-px-lg">
          <q-input label="Senha"></q-input>
          <small>*Insira somente se deseja alterar</small>
        </div>
      </div>

      <div class="row q-mt-md">
        <div class="col-3 q-px-lg">
          <q-select
            label="Gênero"
            v-model="user_edit.gender"
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
          <q-input
            type="number"
            label="Idade"
            v-model="user_edit.age"
          ></q-input>
        </div>
      </div>
      <div class="col-12 justify-end q-px-lg q-mt-lg">
        <q-btn @click="onSave()" class="text-green-8">Salvar</q-btn>
      </div>
    </q-card>
  </div>
</template>

<script>
import axios from "axios";
import { useQuasar } from "quasar";

export default {
  props: {
    user: {
      type: Object,
      required: true,
    },
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

  data() {
    return {
      user_edit: JSON.parse(JSON.stringify(this.user)),
    };
  },

  methods: {
    onSave() {
      axios({
        method: "PUT",
        url: "http://localhost:8081/users",
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
        data: this.user_edit,
      })
        .then((response) => {
          if (response.data == "success") {
            this.showNotify(
              "positive",
              "Seu perfil foi atualizado com sucesso."
            );
            this.$emit("onGetUser");
          } else {
            this.showNotify(
              "negative",
              "Ocorreu uma falha ao atualizar o seu perfil."
            );
          }
        })
        .catch((error) => {
          this.showNotify(
            "negative",
            "Ocorreu uma falha ao atualizar o seu perfil."
          );
        });
    },
  },
};
</script>

<style></style>
