<template>
  <tr>
    <td>{{ id }}</td>
    <td>{{ nome }}</td>
    <td>{{ matricula }}</td>
    <td>{{ email }}</td>
    <td>{{ cpf }}</td>
    <td class="content-center" @click="showModal()">
      <i class="fa-solid fa-pencil"></i>
    </td>
    <td class="content-center" @click="deleteUser(id)">
      <i class="fa-solid fa-trash"></i>
    </td>
    <Modal class="modal-container" v-show="isModalVisible" @close="closeModal" :propId="id" :propIsUpdate="true">
      <template v-slot:header> Atualizar dados </template>
    </Modal>
  </tr>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  name: "User",
  components: {
    Modal,
  },
  data() {
    return {
      id: this.user.id,
      nome: this.user.nome,
      matricula: this.user.matricula,
      email: this.user.email,
      cpf: this.user.cpf,
      isModalVisible: false,
    };
  },
  props: {
    user: {
      type: Object,
    },
  },
  methods: {
    deleteUser(id) {
      this.$parent.deleteUser(id);
      this.$el.parentNode.removeChild(this.$el);
    },
    updateUser(id, userNome, userMatricula, userEmail, userCpf) {
      this.nome = userNome
      this.matricula = userMatricula
      this.email = userEmail
      this.cpf = userCpf
      this.$parent.updateUser(id, userNome, userMatricula, userEmail, userCpf);
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
};
</script>

<style scoped>
td {
  padding: 10px;
  text-align: left;
}

.content-center {
  text-align: center;
}
.content-center:hover {
  color: rgb(216, 67, 67);
  cursor: pointer;
}

.modal-container {
  position: absolute;
}
</style>
