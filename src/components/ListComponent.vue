<template>
  <div class="row">
    <div class="col-md-12">
      <h1 class="text-center mb-4">Student List</h1>
      <input
        class="form-control mb-3 search"
        type="search"
        placeholder="Search"
        aria-label="Search"
        v-model="search"
      />
      <table class="table table-striped">
        <thead class="thead-dark text-center">
          <tr>
            <th>NIS</th>
            <th>Name</th>
            <th>Email</th>
            <th>Age</th>
            <th>Address</th>
            <th>Phone</th>
            <th>Last Update</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody class="text-center">
          <tr v-for="student in filteredList" :key="student._id">
            <td>{{ student.nis }}</td>
            <td>{{ student.name }}</td>
            <td>{{ student.email }}</td>
            <td>{{ student.age }}</td>
            <td>{{ student.address }}</td>
            <td>{{ student.phone }}</td>
            <td>{{ student.date }}</td>
            <td>
              <router-link
                :to="{ name: 'edit', params: { id: student._id } }"
                class="btn btn-success"
                >Edit
              </router-link>
              <button
                @click.prevent="deleteStudent(student._id)"
                class="btn btn-danger"
              >
                Delete
              </button>
              <router-link
                :to="{ name: 'detail', params: { id: student._id } }"
                class="btn btn-primary"
                >Detail
              </router-link>
            </td>
          </tr>
        </tbody>
      </table>
      <div class="col text-center">
        <router-link
          :to="{ name: 'home' }"
          class="btn btn-primary mt-3 btn-lg px-5"
          >Add
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      search: "",
      Students: [],
      apiURL: null,
    };
  },
  mounted() {
    this.getStudent();
  },
  methods: {
    deleteStudent(id) {
      let apiURL = `http://localhost:4000/api/delete-student/${id}`;
      let indexOfArrayItem = this.Students.findIndex((i) => i._id === id);
      if (window.confirm("Do you really want to delete?")) {
        axios
          .delete(apiURL)
          .then(() => {
            this.Students.splice(indexOfArrayItem, 1);
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
    getStudent() {
      let apiURL = "http://localhost:4000/api";
      axios
        .get(apiURL)
        .then((res) => {
          this.Students = res.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  computed: {
    filteredList() {
      return this.Students.filter((student) => {
        return student.name.toLowerCase().includes(this.search.toLowerCase()) || student.age.toLowerCase().includes(this.search.toLowerCase())||student.nis.toLowerCase().includes(this.search.toLowerCase())||student.phone.toLowerCase().includes(this.search.toLowerCase())||student.address.toLowerCase().includes(this.search.toLowerCase())||student.date.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
};
</script>

<style>
.btn-success {
  margin-right: 7px;
}

.btn-primary {
  margin-left: 7px;
}

thead {
  background-color: #404447;
  color: white;
}

.search {
  width: 20%;
}
</style>
