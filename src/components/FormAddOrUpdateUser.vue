<template>
  <form action="">
    <div class="input">
      <label for="input-nome">Nome:</label>
      <input
        type="text"
        id="input-nome"
        name="input-nome"
        placeholder="João Aristides"
        v-model="inputNome"
        required
      />
    </div>
    <div class="input">
      <label for="input-matricula">Matricula:</label>
      <input
        v-mask="'#######'"
        type="text"
        id="input-matricula"
        name="input-matricula"
        placeholder="6483679"
        v-model="inputMatricula"
        required
      />
    </div>
    <div class="input">
      <label for="input-email">Email:</label>
      <input
        type="email"
        id="input-email"
        name="input-email"
        placeholder="joaoaristides@gmail.com"
        v-model="inputEmail"
        required
      />
    </div>
    <div class="input">
      <label for="input-cpf">CPF:</label>
      <input
        v-mask="'###.###.###-##'"
        type="text"
        id="input-cpf"
        name="input-cpf"
        placeholder="01234567890"
        v-model="inputCpf"
        required
      />
    </div>
  </form>
</template>

<script>
export default {
  name: "FormAddOrUpdateUser",
  data() {
    return {
      id: this.propId,
      isUpdate: this.propIsUpdate,
      inputNome: this.inputNome,
      inputMatricula: this.inputMatricula,
      inputEmail: this.inputEmail,
      inputCpf: this.inputCpf,
    };
  },
  props: {
    propId: Number,
    propIsUpdate: Boolean,
  },
  methods: {
    async updateUser() {
      this.$parent.updateUser(
        this.id,
        this.inputNome,
        this.inputMatricula,
        this.inputEmail,
        this.inputCpf
      );
    },
    async addUser() {
      this.$parent.addUser(
        this.inputNome,
        this.inputMatricula,
        this.inputEmail,
        this.inputCpf
      );
    },
  },
};
</script>

<style scoped>
</style>