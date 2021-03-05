<template>
  <div class="mb-6">
    <!-- Header -->
    <br>
    <div class="container">
      <nav class="navbar navbar-dark bg-primary">
        <div class="container-fluid">
          <a class="navbar-brand" href="#">
            <img
              src="https://capital.sec.or.th/ssl_client/als_online/logosec.png"
              alt=""
              width="100"
              height="80"
              class="d-inline-block align-top"
            />
            SEC API นิติบุคคล
          </a>

          <form class="d-flex">
            <input
              class="form-control me-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
            />
            <button class="btn btn-outline-light" type="submit">
              Search
            </button>
          </form>
        </div>
      </nav>
    </div>
    <br>
    <!-- ตารางผู้ใช้งาน -->
    <div class="container">
      <div class="table-container">
        <table class="table table-primary table-bordered border-primary">
          <thead>
            <tr>
              <th>รหัสนิติบุคคล</th>
              <th>ชื่อนิติบุคคล (ภาษาไทย)</th>
              <th>ชื่อนิติบุคคล (ภาษาอังกฤษ)</th>
              <th>วันที่แก้ไขข้อมูลล่าสุด</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="user in users" :key="user.unique_id">
              <td>{{ user.unique_id }}</td>
              <td>{{ user.name_th }}</td>
              <td>{{ user.name_en }}</td>
              <td>{{ user.last_upd_date }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  mounted() {
    this.getUser();
  },
  methods: {
    getUser() {
      axios
        .get(
          "https://api.sec.or.th/LicenseCheck/licensee/company?key=bf9ec9f3df57487786ecbca57d7507ed"
        )
        .then((response) => {
          this.users = response.data;
        });
    },
  },
  data() {
    return {
      users: [],
      user: {
        unique_id: "",
        name_th: "",
        name_en: "",
        last_upd_date: "",
      },
    };
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Prompt&display=swap");
* {
  font-family: "Prompt", sans-serif;
}
body {
  font: 15px/1.8 "Poppins", sans-serif !important;
}

.table td,
.table th {
  padding: 20px !important;
}
.logo {
  width: 200px;
}
</style>
