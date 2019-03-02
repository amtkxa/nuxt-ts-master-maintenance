<template>
  <div>
    <v-toolbar flat color="white">
      <v-toolbar-title>My CRUD</v-toolbar-title>
      <v-divider class="mx-2" inset vertical></v-divider>
      <v-spacer></v-spacer>
      <!-- ダイアログ画面 -->
      <v-dialog v-model="dialog" :max-width="options.width">
        <v-btn slot="activator" color="primary" dark class="mb-2">Create New User</v-btn>
        <v-card>
          <v-card-title>
            <span class="headline">{{ formTitle }}</span>
          </v-card-title>

          <v-card-text>
            <v-container grid-list-md>
              <v-layout wrap>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedUser.id" label="ID"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedUser.first_name" label="First Name"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedUser.last_name" label="Last Name"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedUser.gender" label="Gender"></v-text-field>
                </v-flex>
                <v-flex xs12 sm6 md4>
                  <v-text-field v-model="editedUser.ip_address" label="IP Address"></v-text-field>
                </v-flex>
              </v-layout>
            </v-container>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" flat @click="close">Cancel</v-btn>
            <v-btn color="blue darken-1" flat @click="save">Save</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-toolbar>
    <!-- データテーブル -->
    <v-data-table :headers="headers" :items="people" class="elevation-5">
      <template slot="items" slot-scope="props">
        <td>{{ props.item.id }}</td>
        <td class="text-xs-right">{{ props.item.first_name }}</td>
        <td class="text-xs-right">{{ props.item.last_name }}</td>
        <td class="text-xs-right">{{ props.item.gender }}</td>
        <td class="text-xs-right">{{ props.item.ip_address }}</td>
        <td class="justify-center layout px-0">
          <v-icon small class="mr-2" @click="editUser(props.item)">edit</v-icon>
          <v-icon small @click="deleteUser(props.item)">delete</v-icon>
        </td>
      </template>
      <template slot="no-data">
        <v-btn color="primary">Reset</v-btn>
      </template>
    </v-data-table>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "nuxt-property-decorator";
import { State } from "vuex-class";
import { Person } from "~/types";

@Component({})
export default class UserList extends Vue {
  @Prop() people: Person;
  data() {
    return {
      dialog: false,
      options: {
        width: 500
      },
      headers: [
        { text: "ID", value: "id" },
        { text: "First Name", value: "first_name" },
        { text: "Last Name", value: "last_name" },
        { text: "Gender", value: "gender" },
        { text: "IP Address", value: "ip_address" }
      ],
      defaultUser: {
        id: 0,
        first_name: "",
        last_name: "",
        gender: "",
        ip_address: ""
      },
      editedUser: {
        id: 0,
        first_name: "",
        last_name: "",
        gender: "",
        ip_address: ""
      }
    };
  }

  editedIndex: -1;

  private get formTitle() {
    return this.editedIndex === -1 ? "New Item" : "Edit Item";
  }

  private close() {}
  private save() {}
}
</script>

<style scoped>
</style>
