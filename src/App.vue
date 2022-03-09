<template>
  <div id="app">
    <table class="main-table">
      <thead>
        <tr>
          <th class="main-table-head">id</th>
          <th class="main-table-head">nome</th>
          <th class="main-table-head">matricula</th>
          <th class="main-table-head">email</th>
          <th class="main-table-head">cpf</th>
          <th class="main-table-head data-manipulation">Editar</th>
          <th class="main-table-head data-manipulation">Apagar</th>
        </tr>
      </thead>
      <User v-for="user in users" :key="user.id" :user="user" />
    </table>
    <button class="btn btn-blue" @click="showModal()">Adicionar Usuário</button>
    <Modal
      class="modal-container"
      v-show="isModalVisible"
      @close="closeModal"
      :propIsUpdate="false"
      :data="{}"
    >
      <template v-slot:header> Adicionar dados </template>
    </Modal>
  </div>
</template>

<script>
import User from "./components/User.vue";
import Modal from "./components/Modal.vue";
export default {
  name: "App",
  components: {
    User,
    Modal,
  },
  data() {
    return {
      users: null,
      isModalVisible: false,
    };
  },
  methods: {
    async getUser(id) {
      const req = await fetch("http://localhost:3000/usuarios/" + id);
      const data = await req.json();
      return data;
    },
    async getUsers() {
      const req = await fetch("http://localhost:3000/usuarios");
      const data = await req.json();
      return data;
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
      console.log(res)
      return res.status;
    },
    async addUser(userNome, userMatricula, userEmail, userCpf) {
      console.log("inside App", userNome, userMatricula, userEmail, userCpf);

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
      if (res.status < 400) {
        const data = await this.getUsers();
        window.alert('Dados adicionados com sucesso!')
        this.users = data;
      }
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
  },
  async mounted() {
    const res = this.getUsers();
    this.users = await res;
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
  background: linear-gradient(90deg, #077c20, #92b496);
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
thead {
  background: #00254b;
  color: white;
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
  min-width: 40px;
  max-width: 200px;
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
.btn-blue {
  color: white;
  background: #00254b;
}
.btn:hover {
  cursor: pointer;
  transform: scale(1.01);
  box-shadow: 6px 8px 10px rgba(0, 0, 0, 0.3);
}
</style>
