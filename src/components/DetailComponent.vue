<template>
    <div >
        <div>
            <h1 class="text-center">Detail Student</h1>
            <table class="table mt-4 detail">
                <tbody>
                <tr><td>Name</td>
                <td>:</td>
                <td>{{student.name}}</td></tr>
                <tr><td>Email</td>
                <td>:</td>
                <td>{{student.email}}</td></tr>
                <tr><td>Age</td>
                <td>:</td>
                <td>{{student.age}}</td></tr>
                <tr><td>Address</td>
                <td>:</td>
                <td>{{student.address}}</td></tr>
                <tr><td>Phone</td>
                <td>:</td>
                <td>{{student.phone}}</td></tr>
                <tr><td>Last Update</td>
                <td>:</td>
                <td>{{student.date}}</td></tr>
            </tbody>
            </table>
            <div class="col text-center">
            <router-link :to="{name: 'view'}" class="btn btn-danger mt-3 btn-lg px-5">Back
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
            student: { }
        }
    },
    created() {
        let apiURL = `http://localhost:4000/api/edit-student/${this.$route.params.id}`;

        axios.get(apiURL).then((res) => {
            this.student = res.data;
        })
    }
}
</script>

<style>

    .detail td{
        padding-bottom: 20px;
    }
</style>