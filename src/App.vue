<template>
  <v-app>
    <div class="">
      <div class="logo">
        <v-img class="img-logo" src="./assets/images/logo.png" />
      </div>

      <div class="header">
        <v-form ref="form" class="contaner-header" lazy-validation>
          <v-text-field
            v-model="Name"
            label="Name"
            placeholder="Name"
            requiment
          ></v-text-field>
          <v-select
            :items="items_office"
            label="Office"
            placeholder="Office"
            requiment
          ></v-select>

          <v-autocomplete
            v-model="values_skills"
            :items="item_skills"
            chips
            deletable-chips
            label="Skills"
            multiple
          >
          </v-autocomplete>

          <v-btn block class="white--text btn-search" width="260" height="36"
            >SEARCH</v-btn
          >
        </v-form>
      </div>

      <div class="body">
        <template>
          <v-toolbar flat color="#f2f2f2">
            <v-toolbar-title>Results : <span>10</span> </v-toolbar-title>
            <v-divider class="mx-4" inset vertical></v-divider>
            <v-spacer></v-spacer>
            <v-dialog v-model="dialog" max-width="500px">
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="primary"
                  size="12px"
                  class="mb-1"
                  v-bind="attrs"
                  v-on="on"
                >
                  New Employee
                </v-btn>
              </template>

              <v-card>
                <v-card-title>
                  <span class="headline">{{ formTitle }}</span>
                </v-card-title>
              </v-card>
            </v-dialog>
          </v-toolbar>
        </template>

        <v-data-table :headers="headers" :items="desserts" class="elevation-1">
          <template v-slot:[`item.images`]="{ item }">
            <v-avatar width="70" height="70">
              <img :src="getImg(item.images)" />
            </v-avatar>
          </template>

          <template v-slot:[`item.office`]="{ item }">
            <p class="">{{ item.office }}</p>
          </template>

          <template v-slot:[`item.fullname`]="{ item }">
            <h3 class="">{{ item.fullname.name }}</h3>
            <p class="des-fullname">{{ item.fullname.description }}</p>
          </template>

          <template v-slot:[`item.skills`]="{ item }">
            <v-list-item-title>
              <strong>Backend: </strong>
              <span> {{ item.skills.backend }} </span>
            </v-list-item-title>

            <v-list-item-title>
              <strong class="">Frontend: </strong>
              <span> {{ item.skills.frontend }} </span>
            </v-list-item-title>
            <v-list-item-title>
              <strong class="">Database: </strong>
              <span> {{ item.skills.database }} </span>
            </v-list-item-title>
          </template>

          <template class="btn-color" v-slot:[`item.actions`]="{}">
            <v-btn small class="mr-2"> Edit </v-btn>
            <v-spacer></v-spacer>
            <v-btn mall depressed color="error"> Delete </v-btn>
          </template>
        </v-data-table>
      </div>
    </div>
  </v-app>
</template>

<script>
import { dataList } from "../data.json";
export default {
  name: "App",

  components: {},

  data: () => ({
    dialog: false,
    Name: "John Doe",
    items_office: ["DAD", "b", "c", "d"],

    item_skills: ["Java", "Python", "HTML/CSS", "Postgres"],
    values_skills: ["Java", "Python", "Postgres", "HTML/CSS"],

    headers: [
      {
        text: "#",
        sortable: false,
        value: "stt",
      },
      { text: "Staff ID", value: "id", sortable: false },
      { text: "Office", value: "office", sortable: false },
      { text: "", value: "images", sortable: false },
      { text: "Full Name", value: "fullname", sortable: false },
      { text: "Skills", value: "skills", sortable: false },
      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    editedIndex: -1,
  }),
  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "New Item" : "Edit Item";
    },
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = dataList;
    },
    getImg(images) {
      return require(`${images}`);
    },
  },
};
</script>
<style scoped>
.logo {
  position: relative;
  width: 100%;
  height: 60px;
  left: 0px;
  top: 0px;

  background: #ffffff;
}
.img-logo {
  position: absolute;
  width: 156px;
  height: 60px;
  left: 15px;
  top: 0px;
}
.header {
  position: absolute;
  width: 300px;
  height: 1120px;
  left: -1px;
  top: 60px;

  background: #ffffff;
  border: 1px solid #e5e5e5;
  box-sizing: border-box;
}
.contaner-header {
  padding: 20px;
}

.body {
  position: absolute;
  background: #f2f2f2;
  width: 1620px;
  height: auto;
  left: 300px;
  padding: 69px 273px 110px 268px;
}

.v-data-table >>> tr:nth-child(even) {
  background-color: #edf0f5;
}
.v-btn:not(.v-btn--round).v-size--default {
  width: 120px;
  height: 30px;

  background: #1867c0;
  border-radius: 5px;
}
.v-btn {
  width: 120px;
  height: 23px;
  border: 1px solid #e5e5e5;
  box-sizing: border-box;
  border-radius: 5px !important;
}
.des-fullname {
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
  display: -webkit-box;

  width: 241px;
  height: 42px;
  font-family: Roboto;
  font-style: normal;
  font-weight: normal;
  font-size: 12px;
  line-height: 14px;
}

.v-application p {
  margin-bottom: 10px;
  margin-top: 5px;
}
b,
strong {
  font-weight: bolder;
}
.v-list-item__title {
  width: 265px;
  font-size: 12px;
}
.v-toolbar__title {
  font-size: 12px;
}
.v-btn {
  font-size: 12px !important;
}
.v-btn--contained {
  background: #ffffff !important;
  box-shadow: none;
  margin-bottom: 10px;
}

.btn-search {
  background-color: #1867c0 !important;
}
</style>