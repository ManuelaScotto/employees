<template>
  <div id="employee-table">
    <p v-if="employees.length < 1" class="empty-table">No employees</p>
    <table v-else>
      <thead>
        <tr>
          <th>Nome dipendente</th>
          <th>Email</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="employee in employees" :key="employee.id">
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.name" />
          </td>
          <td v-else>
            {{ employee.name.charAt(0).toUpperCase() + employee.name.slice(1) }}
          </td>
          <td v-if="editing === employee.id">
            <input type="text" v-model="employee.email" />
          </td>
          <td v-else>{{ employee.email.toLowerCase() }}</td>
          <td v-if="editing === employee.id">
            <button @click="editEmployee(employee)">Salva</button>
          </td>
          <td v-else>
            <button @click="editMode(employee.id)">Modifica</button>
            <button @click="$emit('delete:employee', employee.id)">
              Cancella
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "employee-table",
  props: ["employees"],
  data() {
    return {
      editing: null,
    };
  },
  methods: {
    editMode(id) {
      this.editing = id;
    },
    editEmployee(employee) {
      if (employee.name === "" || employee.email === "") return;
      this.$emit("edit:employee", employee.id, employee);
      this.editing = null;
    },
  },
};
</script>

<style scoped>
table {
  margin-top: 20px;
}
button {
  margin: 0 0.5rem 0 0;
}
@media screen and (max-width: 611px) {
  button {
    margin-bottom: 0.5rem;
  }
}
input {
  margin: 0;
}
</style>