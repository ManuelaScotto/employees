<template>
  <div id="app" class="small-container">
    <h1>DIPENDENTI</h1>
    <employee-form @add:employee="addEmployee" />
    <employee-table
      :employees="employees"
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />
  </div>
</template>


<script>
// importiamo il nostro componente header
import EmployeeTable from "@/components/EmployeeTable.vue";
import EmployeeForm from "@/components/EmployeeForm.vue";

//ed esportiamo per la creazione del file compilato tutte le regole di default
export default {
  name: "app",
  components: {
    //chiave di vue per inserire componenti
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    //nei componenti il data è una funzione che restituisce le nostre variabili sotto forma di oggetto
    return {
      employees: [
        {
          id: 1,
          name: "Richard Hendricks",
          email: "richard@piedpiper.com",
        },

        {
          id: 2,
          name: "Bertram Gilfoyle",
          email: "gilfoyle@piedpiper.com",
        },
        {
          id: 3,
          name: "Dinesh Chugtai",
          email: "dinesh@piedpiper.com",
        },
        {
          id: 4,
          name: "Leanne Graham",
          email: "Sincere@april.biz",
        },
        {
          id: 5,
          name: "Antonette",
          email: "Shanna@melissa.tv",
        },
      ],
    };
  },
  mounted() {
    //possiamo caricare i dati che ci servono prima di montare il componente
    this.getEmployees();
  },
  methods: {
    /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
    // CHIAMATA ASINCRONA PER INSERIRE GLI IMPIEGATI (UTILIZZO FETCH)
    /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

    // async getEmployees() {
    //   try {
    //     const response = await fetch(
    //       "https://jsonplaceholder.typicode.com/users"
    //     );
    //     const data = await response.json();
    //     this.employees = data;
    //   } catch (error) {
    //     console.error(error);
    //   }
    // },
    // async addEmployee(employee) {
    //   try {
    //     const response = await fetch(
    //       "https://jsonplaceholder.typicode.com/users",
    //       {
    //         method: "POST",
    //         body: JSON.stringify(employee),
    //         headers: { "Content-type": "application/json; charset=UTF-8" },
    //       }
    //     );
    //     const data = await response.json();
    //     this.employees = [...this.employees, data];
    //   } catch (error) {
    //     console.error(error);
    //   }
    // },
    // async editEmployee(id, updatedEmployee) {
    //   try {
    //     const response = await fetch(
    //       `https://jsonplaceholder.typicode.com/users/${id}`,
    //       {
    //         method: "PUT",
    //         body: JSON.stringify(updatedEmployee),
    //         headers: { "Content-type": "application/json; charset=UTF-8" },
    //       }
    //     );
    //     const data = await response.json();
    //     this.employees = this.employees.map((employee) =>
    //       employee.id === id ? data : employee
    //     );
    //   } catch (error) {
    //     console.error(error);
    //   }
    // },
    // async deleteEmployee(id) {
    //   try {
    //     await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
    //       method: "DELETE",
    //     });
    //     this.employees = this.employees.filter(
    //       (employee) => employee.id !== id
    //     );
    //   } catch (error) {
    //     console.error(error);
    //   }
    // },

    /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
    // INSERISCO I DIPENDENTI A MANO (SENZA UTILIZZARE FETCH)
    /////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      this.employees = [...this.employees, newEmployee];
    },
    deleteEmployee(id) {
      this.employees = this.employees.filter((employee) => employee.id !== id);
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map((employee) =>
        employee.id === id ? updatedEmployee : employee
      );
    },
  },
};
</script>

<style>
body {
  background: linear-gradient(-15deg, #8076c0, #71d7ff);
  min-height: 100vh;
}
@media screen and (max-width: 422px) {
  body {
    min-width: 400px;
  }
}
button {
  background: slategray;
  border: 1px solid slategray;
}
.small-container {
  max-width: 880px;
}
</style>
