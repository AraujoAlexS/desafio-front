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
    <Modal
      class="modal-container"
      v-show="isModalVisible"
      @close="closeModal"
      :propIsUpdate="true"
      :data="this.user"
      
    >
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
    async deleteUser(id) {
      this.$parent.deleteUser(id);
      this.$el.parentNode.removeChild(this.$el);
    },
    async updateUser(id, userNome, userMatricula, userEmail, userCpf) {
      const res = await this.$parent.updateUser(
        id,
        userNome,
        userMatricula,
        userEmail,
        userCpf
      );
      console.log(res);
      if (res < 400) {
        window.alert("Update realizado com sucesso");
        this.nome = userNome;
        this.matricula = userMatricula;
        this.email = userEmail;
        this.cpf = userCpf;
      }
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
  transition: all ease-in-out 0.2s;
}
.content-center:hover {
  color: rgb(216, 67, 67);
  cursor: pointer;
  transform: scale(1.15);
}

.modal-container {
  position: absolute;
}
</style>
