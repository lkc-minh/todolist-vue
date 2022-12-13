<template>
  <div class="TodoList mt-10">
    <AddTodoModal :todoList="todoList" />
    <InfoTodoModal
      v-model="showInfo"
      :showInfo="showInfo"
      @setClose="showInfo = false"
      :dataInfo="dataInfo"
    />
    <EditTodoModal
      v-model="showEdit"
      :dataEdit="dataEdit"
      @setCloseEdit="showEdit = false"
      @update="(title, id) => handleUpdate(title, id)"
    />
    <v-container>
      <v-text-field
        label="Search"
        hide-details="auto"
        v-model="searchText"
      ></v-text-field>
      <v-table hover class="Todo_table mt-6">
        <thead>
          <tr>
            <th class="text-left">STT</th>
            <th class="text-left">Title</th>
            <th class="text-left">Status</th>
            <th class="text-left">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(todo, index) in todoListFiltered" :key="todo.id">
            <td>{{ index + 1 }}</td>
            <td>{{ todo.title }}</td>
            <td>
              <v-checkbox
                v-model="todo.completed"
                density
                color="success"
                hide-details
              ></v-checkbox>
            </td>
            <td class="Todo_action">
              <v-tooltip text="Information" location="bottom">
                <template v-slot:activator="{ props }">
                  <v-btn
                    color="primary "
                    icon="mdi-account"
                    v-bind="props"
                    size="x-small"
                    @click="handleGetData(todo)"
                  ></v-btn>
                </template>
              </v-tooltip>

              <v-tooltip text="Edit" location="bottom">
                <template v-slot:activator="{ props }">
                  <v-btn
                    color="warning"
                    icon="mdi-pencil"
                    size="x-small"
                    v-bind="props"
                    @click="handleShowEdit(todo)"
                  ></v-btn>
                </template>
              </v-tooltip>
              <v-tooltip text="Delete" location="bottom">
                <template v-slot:activator="{ props }">
                  <v-btn
                    color="error"
                    v-bind="props"
                    icon="mdi-delete"
                    size="x-small"
                    @click="handleDelete(todo.id)"
                  ></v-btn>
                </template>
              </v-tooltip>
            </td>
          </tr>
        </tbody>
      </v-table>
    </v-container>
  </div>
</template>

<script>
import AddTodoModal from "@/components/AddTodoModal.vue";
import InfoTodoModal from "@/components/InfoTodoModal.vue";
import EditTodoModal from "@/components/EditTodoModal.vue";

export default {
  components: { AddTodoModal, InfoTodoModal, EditTodoModal },
  data() {
    return {
      showInfo: false,
      showEdit: false,
      searchText: "",
      dataEdit: {},
      dataInfo: {},
      todoList: [
        { id: 1, title: "Coding", completed: false },
        { id: 2, title: "Fixing bugs", completed: false },
        { id: 3, title: "Reading books", completed: true },
      ],
    };
  },
  computed: {
    todoListFiltered() {
      return this.todoList.filter((todo) =>
        todo.title.toLowerCase().includes(this.searchText.toLowerCase())
      );
    },
  },
  methods: {
    handleDelete(id) {
      this.todoList = this.todoList.filter((todo) => todo.id !== id);
    },
    handleGetData(data) {
      this.showInfo = true;
      this.dataInfo = data;
    },
    handleShowEdit(data) {
      this.showEdit = true;
      this.dataEdit = data;
    },
    handleUpdate(title, id) {
      this.todoList.forEach((todo, index) => {
        if (todo.id === id) {
          this.todoList[index].title = title;
        }
      });
    },
  },
};
</script>
<style>
.Todo_table {
  border: 1px solid lightgray;
  border-radius: 4px;
}
.Todo_action {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
