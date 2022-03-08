<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal-header" id="modalTitle">
          <slot name="header"> </slot>
          <button
            type="button"
            class="btn-close"
            @click="close"
            aria-label="Close modal"
          >
            <i class="fa-solid fa-times" />
          </button>
        </header>
        <section class="modal-body" id="modalDescription">
          <slot name="body"> </slot>
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
        </section>

        <footer class="modal-footer">
          <slot name="footer"> </slot>
          <button
            type="button"
            class="btn btn-green"
            @click="isUpdate ? updateUser() : addUser()"
            aria-label="Close modal"
          >
            Confirmar
          </button>
          <button
            type="button"
            class="btn btn-red"
            @click="close"
            aria-label="Close modal"
          >
            Cancelar
          </button>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import { mask } from "vue-the-mask";
export default {
  name: "Modal",
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
  directives: { mask },
  methods: {
    close() {
      this.$emit("close");
    },
    async updateUser() {
      this.$parent.updateUser(
        this.id,
        this.inputNome,
        this.inputMatricula,
        this.inputEmail,
        this.inputCpf
      );

      this.close();
    },
    async addUser() {
      this.$parent.addUser(
        this.inputNome,
        this.inputMatricula,
        this.inputEmail,
        this.inputCpf
      );
      this.close();
    },
    print(str) {
      console.log(str);
    },
  },
};
</script>


<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
}

.modal-body {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 20px 10px;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn {
  color: white;
  border-radius: 2px;
  padding: 3px;
  margin: 2px;
  box-shadow: 0px 0px 0px rgba(0, 0, 0, 0.3);
}

.btn:hover {
  transform: scale(1.01);
  box-shadow: 2px 4px 6px rgba(0, 0, 0, 0.3);
}
.btn-green {
  background: #4aae9b;
  border: 1px solid #4aae9b;
}
.btn-red {
  background: rgb(216, 67, 67);
  border: 1px solid rgb(216, 67, 67);
}
.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s ease;
}

.input {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-bottom: 10px;
}

input {
  margin: 5px 0;
  padding: 5px;
  border-radius: 4px;
  border: 1px solid #4aae9b;
}
input:focus {
  outline: none;
}
label {
  color: #4aae9b;
}
</style>
