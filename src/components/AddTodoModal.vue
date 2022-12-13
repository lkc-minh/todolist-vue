<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-container>
    <v-row>
      <v-dialog v-model="dialog" persistent max-width="600px">
        <template v-slot:activator="{ on, attrs }">
          <v-btn
            color="blue"
            dark
            v-bind="attrs"
            v-on="on"
            @click="handleOpenModal"
            class="ml-4"
          >
            Add a new todo
          </v-btn>
        </template>
        <v-card>
          <v-card-title>
            <span class="text-h5">New todo</span>
          </v-card-title>
          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" sm="12" md="12">
                  <v-text-field
                    v-model.trim="title"
                    label="Title"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="dialog = false">
              Close
            </v-btn>
            <v-btn color="blue darken-1" text @click="handleAddTodo">
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </v-container>
</template>

<script>
import { v4 } from "uuid";
export default {
  data: () => ({
    dialog: false,
  }),
  props: ["todoList"],
  methods: {
    handleOpenModal() {
      this.dialog = true;
    },

    handleAddTodo() {
      const newTodo = {
        id: v4(),
        title: this.title,
        completed: false,
      };

      this.$props.todoList.unshift(newTodo);
      this.title = "";
      this.dialog = false;
    },
  },
};
</script>
