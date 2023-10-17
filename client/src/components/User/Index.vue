<template>
  <div>
    <h2>Get all users</h2>
    <p><button v-on:click="logout">Logout</button></p>
    <h4>จํานวนผู้ใช้งาน {{ users.length }}</h4>
    <p>
      <button v-on:click="navigateTo('/user/create')">สร้างผู้ใช้งาน</button>
    </p>
    <div v-for="user in users" v-bind:key="user.id">
      <p>id: {{ user.id }}</p>
      <p>ชือ-นามสกุล: {{ user.name }} - {{ user.lastname }}</p>
      <p>email: {{ user.email }}</p>
      <p>password: {{ user.password }}</p>
      <p>
        <button v-on:click="navigateTo('/user/' + user.id)">
          ดูข้อมูลผู้ใช้
        </button>
        <button v-on:click="navigateTo('/user/edit/' + user.id)">
          แก้ไขข้อมูล
        </button>
        <button v-on:click="deleteUser(user)">ลบข้อมูล</button>
      </p>

      <hr />
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";
export default {
  data() {
    return {
      users: []
    };
  },
  async created() {
    this.users = (await UsersService.index()).data;
  },
  methods: {
    logout() {
      this.$store.dispatch("setToken", null);
      this.$store.dispatch("setUser", null);
      this.$router.push({
        name: "login"
      });
    },
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user) {
      try {
        await UsersService.delete(user);
        this.refreshData();
      } catch (err) {
        console.log(err);
      }
    },
    async refreshData() {
      this.users = (await UsersService.index()).data;
    }
  }
};
</script>
<style scoped></style>
