<template>
  <div class="full-height full-width window-height no-scroll">
    <q-toolbar class="text-danger q-pa-sm bg-orange-5">
      <img src="../assets/logo.png" class="img_logo" />
      <q-toolbar-title class="text-red-10"> UNIRIDE </q-toolbar-title>
      <q-btn
        flat
        label="Dashboard"
        class="text-red-10"
        @click="view = 'dashboard'"
      />
      <q-btn icon="account-key"></q-btn>
      <q-btn
        flat
        icon="account-key"
        class="text-red-10"
        @click="view = 'user'"
      />
    </q-toolbar>

    <div v-if="view == 'dashboard'" class="q-pa-lg full-height">
      <div class="row full-width justify-between">
        <q-card class="box-graph col-3 q-pa-md">
          <table class="charts-css show-heading line show-labels">
            <caption>
              Avaliação do aplicativo
            </caption>

            <thead>
              <tr>
                <th scope="col">Country</th>
                <th scope="col">Gold</th>
                <th scope="col">Silver</th>
                <th scope="col">Bronze</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <th scope="row">Label</th>
                <td>Data</td>
                <td>Data</td>
                <td>Data</td>
              </tr>
            </tbody>
          </table>
        </q-card>
        <q-card class="box-graph col-3 q-pa-md">
          <table class="charts-css bar show-heading q-ma-lg">
            <caption>
              Motoristas no aplicativo
            </caption>

            <thead>
              <tr>
                <th scope="col">Country</th>
                <th scope="col">Gold</th>
                <th scope="col">Silver</th>
                <th scope="col">Bronze</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <th scope="row">USA</th>
                <td>46</td>
                <td>37</td>
                <td>38</td>
              </tr>
              <tr>
                <th scope="row">GBR</th>
                <td>27</td>
                <td>23</td>
                <td>17</td>
              </tr>
              <tr>
                <th scope="row">CHN</th>
                <td>26</td>
                <td>18</td>
                <td>26</td>
              </tr>
            </tbody>
          </table>
        </q-card>
        <q-card class="box-graph col-3 q-pa-md">
          <table class="charts-css bar show-heading">
            <caption>
              Valores das caronas
            </caption>

            <thead>
              <tr>
                <th scope="col">Country</th>
                <th scope="col">Gold</th>
                <th scope="col">Silver</th>
                <th scope="col">Bronze</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <th scope="row">USA</th>
                <td>46</td>
                <td>37</td>
                <td>38</td>
              </tr>
              <tr>
                <th scope="row">GBR</th>
                <td>27</td>
                <td>23</td>
                <td>17</td>
              </tr>
              <tr>
                <th scope="row">CHN</th>
                <td>26</td>
                <td>18</td>
                <td>26</td>
              </tr>
            </tbody>
          </table>
        </q-card>
      </div>
    </div>

    <div v-else>
      <q-table
        title="Usuários"
        :rows="rows"
        :columns="columns"
        row-key="name"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import "charts.css";

export default {
  props: {
    user_id: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      user: {},
      view: "dashboard",
      columns: [
        {
          name: "name",
          required: true,
          label: "Dessert (100g serving)",
          align: "left",
          field: (row) => row.name,
          format: (val) => `${val}`,
          sortable: true,
        },
        {
          name: "calories",
          align: "center",
          label: "Calories",
          field: "calories",
          sortable: true,
        },
        { name: "fat", label: "Fat (g)", field: "fat", sortable: true },
        { name: "carbs", label: "Carbs (g)", field: "carbs" },
        { name: "protein", label: "Protein (g)", field: "protein" },
        { name: "sodium", label: "Sodium (mg)", field: "sodium" },
        {
          name: "calcium",
          label: "Calcium (%)",
          field: "calcium",
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10),
        },
        {
          name: "iron",
          label: "Iron (%)",
          field: "iron",
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10),
        },
      ],

      rows: [
        {
          name: "Frozen Yogurt",
          calories: 159,
          fat: 6.0,
          carbs: 24,
          protein: 4.0,
          sodium: 87,
          calcium: "14%",
          iron: "1%",
        },
        {
          name: "Ice cream sandwich",
          calories: 237,
          fat: 9.0,
          carbs: 37,
          protein: 4.3,
          sodium: 129,
          calcium: "8%",
          iron: "1%",
        },
        {
          name: "Eclair",
          calories: 262,
          fat: 16.0,
          carbs: 23,
          protein: 6.0,
          sodium: 337,
          calcium: "6%",
          iron: "7%",
        },
        {
          name: "Cupcake",
          calories: 305,
          fat: 3.7,
          carbs: 67,
          protein: 4.3,
          sodium: 413,
          calcium: "3%",
          iron: "8%",
        },
        {
          name: "Gingerbread",
          calories: 356,
          fat: 16.0,
          carbs: 49,
          protein: 3.9,
          sodium: 327,
          calcium: "7%",
          iron: "16%",
        },
        {
          name: "Jelly bean",
          calories: 375,
          fat: 0.0,
          carbs: 94,
          protein: 0.0,
          sodium: 50,
          calcium: "0%",
          iron: "0%",
        },
        {
          name: "Lollipop",
          calories: 392,
          fat: 0.2,
          carbs: 98,
          protein: 0,
          sodium: 38,
          calcium: "0%",
          iron: "2%",
        },
        {
          name: "Honeycomb",
          calories: 408,
          fat: 3.2,
          carbs: 87,
          protein: 6.5,
          sodium: 562,
          calcium: "0%",
          iron: "45%",
        },
        {
          name: "Donut",
          calories: 452,
          fat: 25.0,
          carbs: 51,
          protein: 4.9,
          sodium: 326,
          calcium: "2%",
          iron: "22%",
        },
        {
          name: "KitKat",
          calories: 518,
          fat: 26.0,
          carbs: 65,
          protein: 7,
          sodium: 54,
          calcium: "12%",
          iron: "6%",
        },
      ],
    };
  },

  mounted() {
    this.getUser();
  },

  methods: {
    getUser() {
      axios({
        method: "GET",
        url: "http://localhost:8081/users?id=" + this.user_id,
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      })
        .then((response) => {
          if (response.data) this.user = response.data;
        })
        .catch((error) => {
          console.log(error);
        })
        .finally({});
    },
  },
};
</script>

<style>
.img_logo {
  width: 50px;
  height: 50px;
}

.my-chart {
  width: 50px;
  height: 50px;
}
.box-graph {
}
</style>
