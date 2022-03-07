<template>
  <div id="app">
    <table class="main-table">
      <tr>
        <th class="main-table-head">id</th>
        <th class="main-table-head">nome</th>
        <th class="main-table-head">matricula</th>
        <th class="main-table-head">email</th>
        <th class="main-table-head">cpf</th>
        <th class="main-table-head data-manipulation">Editar</th>
        <th class="main-table-head data-manipulation">Apagar</th>
      </tr>
      <User v-for="user in users" :key="user.id" :user="user" />
    </table>
    <button class="btn btn-green" @click="showModal()">Adicionar User</button>
    <Modal
      class="modal-container"
      v-show="isModalVisible"
      @close="closeModal"
      :propId="0"
      :propIsUpdate="false"
    >
      <template v-slot:header> Adicionar dados </template>
    </Modal>
  </div>
</template>

<script>
import User from "./components/User.vue";
import Modal from "./components/Modal.vue"
export default {
  name: "App",
  components: {
    User,
    Modal
  },
  data() {
    return {
      users: [],
      isModalVisible: false,
    };
  },
  methods: {
    async getUsers() {
      const req = await fetch("http://localhost:3000/usuarios");
      const data = await req.json();
      this.users = data;
    },
    async deleteUser(id) {
      fetch("http://localhost:3000/usuarios/" + id, {
        method: "DELETE",
      });
    },
    async updateUser(id, userNome, userMatricula, userEmail, userCpf) {
      const res = await fetch("http://localhost:3000/usuarios/" + id, {
        method: "PUT",
        body: JSON.stringify({
          nome: userNome,
          matricula: userMatricula,
          email: userEmail,
          cpf: userCpf,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      });
      const data = await res.json();
    },
    async addUser(userNome, userMatricula, userEmail, userCpf) {
      console.log("inside App", userNome, userMatricula, userEmail, userCpf)
      
      const res = await fetch("http://localhost:3000/usuarios/", {
        method: "POST",
        body: JSON.stringify({
          nome: userNome,
          matricula: userMatricula,
          email: userEmail,
          cpf: userCpf,
        }),
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      });
      const data = await res.json();
      window.location.reload();
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
  mounted() {
    this.getUsers();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(90deg, #5af362, #92b496);
  height: 100vh;
  display: grid;
  place-items: center;
}

tr:nth-child(2n) {
  background: white;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-items: flex-start;
}

.main-table {
  background: rgb(233, 233, 233);
  border-collapse: collapse;
  padding: 10px;
  border-style: none;
  border-radius: 2px;
  box-shadow: 8px 10px 10px rgba(0, 0, 0, 0.2);
}

.main-table-head {
  padding: 15px 10px;
  width: 170px;
  text-align: left;
  text-transform: capitalize;
  border-bottom: 1px solid black;
}
.data-manipulation {
  padding-left: 0;
  width: 70px;
  text-align: center;
}

.btn {
  border: none;
  border-radius: 2px;
  padding: 15px;
  margin-top: 20px;
  width: 160px;
  text-align: center;
  box-shadow: 4px 6px 8px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease-in-out;
}
.btn:hover{
  cursor: pointer;
  transform: scale(1.01);
  box-shadow: 6px 8px 10px rgba(0, 0, 0, 0.3);
}
</style>
