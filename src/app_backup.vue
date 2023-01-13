<template>
  <!-- NAVBAR KONTEN -->
  <nav class="bg-white border-gray-200 px-2 sm:px-4 py-2.5 rounded dark:bg-gray-900">
    <div class="container flex flex-wrap items-center justify-between mx-auto">
      <a>CRUD</a>
      <button data-collapse-toggle="navbar-default" type="button"
        class="inline-flex items-center p-2 ml-3 text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
        aria-controls="navbar-default" aria-expanded="false">
        <span class="sr-only">Open main menu</span>
        <svg class="w-6 h-6" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20"
          xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd"
            d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
            clip-rule="evenodd"></path>
        </svg>
      </button>
      <div class="hidden w-full md:block md:w-auto" id="navbar-default">
        <ul
          class="flex flex-col p-4 mt-4 border border-gray-100 rounded-lg bg-gray-50 md:flex-row md:space-x-8 md:mt-0 md:text-sm md:font-medium md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700">
          <li>
            <a href="#"
              class="block py-2 pl-3 pr-4 text-white bg-blue-700 rounded md:bg-transparent md:text-white-700 md:p-0 dark:text-white"
              aria-current="page">Home</a>
          </li>
          <li>
            <a href="#"
              class="block py-2 pl-3 pr-4 text-gray-700 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-gray-400 md:dark:hover:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent">About</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <!-- -----END---- -->

  <!-- DIV KESELURUHAN -->
  <div class="containerdiv">
    <!-- TABLE MENAMPILKAN DATA -->
    <table class="border-collapse">
      <thead>
        <tr>
          <th class="border py-2 px-4 text-center text-sm font-medium">ID</th>
          <th class="border py-2 px-4 text-center text-sm font-medium">Nama</th>
          <th class="border py-2 px-4 text-center text-sm font-medium">Email</th>
          <th class="border py-2 px-4 text-center text-sm font-medium">Umur</th>
          <th class="border py-2 px-4 text-center text-sm font-medium">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td class="border py-2 px-4 text-center">{{ user.id }}</td>
          <td class="border py-2 px-4 text-center">{{ user.nama }}</td>
          <td class="border py-2 px-4 text-center">{{ user.email }}</td>
          <td class="border py-2 px-4 text-center">{{ user.umur }}</td>
          <td class="border py-2 px-4 text-center">
            <button
              class="group inline-flex items-center justify-center rounded-full py-2 px-4 text-sm font-semibold focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 bg-slate-900 text-white hover:bg-slate-700 hover:text-slate-100 active:bg-slate-800 active:text-slate-300 focus-visible:outline-slate-900"
              @click="selectUser(user)">Select</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <!-- -----END---- -->

  <!-- TABLE CREATE -->
  <div class="containerdiv">
    <div class="h-20 content-start ...">
      <table class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-300 rounded-xl dark:text-gray-400">
        <thead class="border-b">
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <td>Nama: </td>
              <td>
                <input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="text" id="nama" v-model="nama" />
              </td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <td>Email:</td>
              <td>
                <input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="email" id="email" v-model="email" />
              </td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <td>Umur:</td>
              <td>
                <input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="number" id="number" v-model="umur" />
              </td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <td colspan="2">
                <button
                  class="group inline-flex items-center justify-center rounded-full py-2 px-4 text-sm font-semibold focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 bg-slate-900 text-white hover:bg-slate-700 hover:text-slate-100 active:bg-slate-800 active:text-slate-300 focus-visible:outline-slate-900"
                  @click.prevent="createUser" type="submit">Create User</button>
              </td>
            </tr>
          </th>
        </thead>
      </table>
    </div>
  </div>
  <!-- -----END---- -->

  <!-- TABLE UPDATE DATA -->
  <div class="containerdiv">
    <div>
      <table v-if="selectedUser"
        class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-300 rounded-xl dark:text-gray-400">
        <thead class="border-b">
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <th for="nama"> Nama: </th>
              <td><input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="text" id="nama" v-model="selectedUser.nama" /></td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <th for="email"> Email: </th>
              <td><input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="email" id="email" v-model="selectedUser.email" /></td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <th for="email"> Umur: </th>
              <td><input
                  class="block w-full p-2 text-gray-900 border border-gray-300 rounded-lg bg-gray-50 sm:text-xs focus:ring-blue-500 focus:border-blue-500 dark:bg-white-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-black dark:focus:ring-blue-500 dark:focus:border-blue-500"
                  type="number" id="number" v-model="selectedUser.umur" /></td>
            </tr>
          </th>
          <th scope="col" class="text-sm font-medium text-black px-6 py-4">
            <tr>
              <td>
                <button
                  class="group inline-flex items-center justify-center rounded-full py-2 px-4 text-sm font-semibold focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 bg-slate-900 text-white hover:bg-slate-700 hover:text-slate-100 active:bg-slate-800 active:text-slate-300 focus-visible:outline-slate-900"
                  type="submit" @click="updateUser(selectedUser.id)">Update User</button>
              </td>
              <td>
                <button
                  class="group inline-flex items-center justify-center rounded-full py-2 px-4 text-sm font-semibold focus:outline-none focus-visible:outline-2 focus-visible:outline-offset-2 bg-slate-900 text-white hover:bg-slate-700 hover:text-slate-100 active:bg-slate-800 active:text-slate-300 focus-visible:outline-slate-900"
                  @click="deleteUser(selectedUser.id)">Delete User</button>
              </td>
            </tr>
          </th>
        </thead>
      </table>
    </div>
  </div>
  <!-- -----END---- -->

  


  <!-- END OF DIV KESELURUHAN -->
</template>
<script>

import axios from 'axios';

export default {
  data() {
    return {
      nama: '',
      email: '',
      umur: '',
      users: [],
      selectedUser: null
    }
  },
  created() {
    this.getUsers();
  },
  methods: {

    async getUsers() {
      try {
        const response = await axios.get('http://localhost:5757/users/');
        this.users = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    async createUser(event) {
      try {
        // prevent form submission
        event.preventDefault();

        const response = await axios.post('http://localhost:5757/users/', {
          nama: this.nama,
          email: this.email,
          umur: this.umur
        });
        this.users.push(response.data);
        this.nama = '';
        this.email = '';
        this.umur = '';
        window.location.reload()
      } catch (error) {
        console.error(error);
      }
    },
    async updateUser(id) {
      try {
        const response = await axios.patch(`http://localhost:5757/users/${id}`, {
          nama: this.selectedUser.nama,
          email: this.selectedUser.email,
          umur: this.selectedUser.umur
        });
        this.selectedUser = response.data;
      } catch (error) {
        console.error(error);
      }
      // Membersihkan data yang tersimpan di properti data selectedUser
      this.selectedUser = null;
    },
    async deleteUser(id) {
      try {
        await axios.delete(`http://localhost:5757/users/${id}`);
        this.users = this.users.filter(user => user.id !== id);
        this.selectedUser = null;
      } catch (error) {
        console.error(error);
      }
    },
    selectUser(user) {
      this.selectedUser = user;
    }
  }
}
</script>

<style>

</style>
