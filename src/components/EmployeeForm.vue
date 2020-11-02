<template>
  <div id="employee-form">
    <form @submit.prevent="handleSubmit">
      <label>Inserisci il nome del dipendente</label>
      <input
        v-model="employee.name"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        @focus="clearStatus"
        @keypress="clearStatus"
        ref="first"
      />
      <label>Inserisci la mail del dipendente</label>
      <input
        v-model="employee.email"
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">
        ❗ Si prega di compilare tutti i dati richiesti
      </p>
      <p v-if="success" class="success-message">
        ✅ Nuovo impiegato aggiunto con successo
      </p>
      <button>
        <span></span>
        <span></span>
        <span></span>
        <span></span>

        Aggiungi
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      this.submitting = true;
      this.clearStatus();

      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }
      this.$emit("add:employee", this.employee);
      this.$refs.first.focus();
      //   this.employee.name = "";
      //   this.employee.email = "";
      this.employee = {
        name: "",
        email: "",
      };
      this.error = false;
      this.success = true;
      setTimeout(() => (this.success = false), 2000);
      this.submitting = false;
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },

    invalidEmail() {
      return this.employee.email === "";
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}
button {
  margin-top: 20px;
  transform: translate(0, 0);
  color: snow;
  padding: 15px 30px;
  font-size: 15px;
  letter-spacing: 2px;
  text-decoration: none;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
  background: #00008b;
  overflow: hidden;
}
button:before {
  content: "";
  position: absolute;
  top: 2px;
  left: 2px;
  bottom: 2px;
  width: 50%;
  background: rgba(255, 255, 255, 0.07);
}
button span:nth-child(1) {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(to right, darkcyan, #00008b);
  animation: animate1 2s linear infinite;
  animation-delay: 0.5s;
}
@keyframes animate1 {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}
button span:nth-child(2) {
  position: absolute;
  top: 0;
  right: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(to bottom, darkcyan, #00008b);
  animation: animate2 2s linear infinite;
  animation-delay: 0.5s;
}
@keyframes animate2 {
  0% {
    transform: translateY(-100%);
  }
  100% {
    transform: translateY(100%);
  }
}
button span:nth-child(3) {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 2px;
  background: linear-gradient(to left, darkcyan, #00008b);
  animation: animate3 2s linear infinite;
  animation-delay: 0.2s;
}
@keyframes animate3 {
  0% {
    transform: translateX(100%);
  }
  100% {
    transform: translateX(-100%);
  }
}
button span:nth-child(4) {
  position: absolute;
  top: 0;
  left: 0;
  width: 2px;
  height: 100%;
  background: linear-gradient(to top, darkcyan, #00008b);
  animation: animate4 2s linear infinite;
  animation-delay: 1s;
}
@keyframes animate4 {
  0% {
    transform: translateY(100%);
  }
  100% {
    transform: translateY(-100%);
  }
}
button:hover {
  color: darkcyan;
}
.error-message {
  color: #d33c40;
}

.success-message {
  color: darkgreen;
}
</style>