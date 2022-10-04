<template>
  <div class="row justify-content-center">
    <div class="col-md-6">
      <h3 class="text-center">Create Student</h3>
      <form @submit.prevent="handleSubmitForm" class="form">
        <div class="form-group">
          <label>Name</label>
          <input
            type="text"
            class="form-control"
            v-model="student.name"
            required
          />
        </div>

        <div class="form-group">
          <label>Email</label>
          <input
            type="email"
            class="form-control"
            v-model="student.email"
            required
          />
        </div>

        <div class="form-group">
          <label>Age</label>
          <input
            type="text"
            class="form-control"
            v-model="student.age"
            required
          />
        </div>

        <div class="form-group">
          <label>Address</label>
          <textarea class="form-control" v-model="student.address" required>
          </textarea>
        </div>

        <div class="form-group">
          <label>Phone</label>
          <input
            type="text"
            class="form-control"
            v-model="student.phone"
            required
          />
        </div>

        <div class="form-group">
          <button class="btn btn-primary btn-block mt-3 px-5">Create</button>
          <router-link :to="{ name: 'view' }" class="btn btn-success mt-3"
            >View
          </router-link>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
export default {
  data() {
    return {
      student: {
        nis: "",
        name: "",
        email: "",
        age: "",
        address: "",
        phone: "",
        date: moment(new Date()).format("DD-MM-YYYY"),
      },
    };
  },
  methods: {
    handleSubmitForm() {
      let apiURL = "http://localhost:4000/api/create-student";

      axios
        .post(apiURL, this.student)
        .then(() => {
          this.$router.push("/view");
          this.student = {
            nis: "",
            name: "",
            email: "",
            age: "",
            address: "",
            phone: "",
            date: moment(new Date()).format("DD-MM-YYYY"),
          };
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>

<style>
.btn-success {
  margin-left: 10px;
}

.form-group {
  margin-bottom: 10px;
}

.form-group label {
  margin-bottom: 10px;
}
</style>
