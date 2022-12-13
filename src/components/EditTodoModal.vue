<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-dialog persistent max-width="600px">
    <v-card>
      <v-card-title>
        <span class="text-h5">Edit todo {{ dataEdit.title }}</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="12" md="12">
              <v-text-field v-model="title" label="Title"></v-text-field>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="handleClose"> Close </v-btn>
        <v-btn color="blue darken-1" @click="handleUpdate(dataEdit.id)" text>
          Update
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    title: "",
  }),
  props: ["dataEdit"],
  updated() {
    this.title = this.$props.dataEdit.title;
    console.log(this.title);
  },
  methods: {
    handleClose() {
      this.$emit("setCloseEdit");
    },
    handleUpdate(id) {
      this.$emit("update", this.title, id);
      this.$emit("setCloseEdit");
    },
  },
};
</script>
