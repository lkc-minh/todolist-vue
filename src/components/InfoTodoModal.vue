<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <v-dialog persistent max-width="600px">
    <v-card>
      <v-card-title class="border-bottom">
        <span class="text-h5">Info todo</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12" sm="12" md="12">
              <p><b>Title:</b> {{ dataInfo.title }}</p>
            </v-col>
            <v-col cols="12" sm="12" md="12">
              <p>
                <b>Status:</b> {{ dataInfo.completed ? "Done" : "Unfinished" }}
              </p>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="handleClose"> Close </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    // dialog: true,
  }),
  props: ["showInfo", "dataInfo"],
  methods: {
    handleClose() {
      this.$emit("setClose");
    },
  },
};
</script>

<style>
.border-bottom {
  border-bottom: 1px solid lightgray;
}
</style>
