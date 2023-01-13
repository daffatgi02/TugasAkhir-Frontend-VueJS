<template>
  <html class="h-full scroll-smooth antialiased [font-feature-settings:'ss01'] js-focus-visible">

  <head>
    <title>Tes Projek</title>
  </head>

  <body class="">
    <div class="m">
      <div>

        <div v-if="showModal" class="fixed top-0 left-0 w-full h-full flex items-center justify-center">
          <div class="bg-white p-6 rounded-md">
            <form @submit.prevent="createUser">
              <div class="mb-2">
                <label class="block text-gray-700 font-medium mb-1">Nama:</label>
                <input v-model="nama" class="border border-gray-400 p-2 rounded-md w-full" />
              </div>
              <div class="mb-2">
                <label class="block text-gray-700 font-medium mb-1">Email:</label>
                <input v-model="email" class="border border-gray-400 p-2 rounded-md w-full" />
              </div>
              <div class="mb-2">
                <label class="block text-gray-700 font-medium mb-1">Umur:</label>
                <input v-model="umur" class="border border-gray-400 p-2 rounded-md w-full" />
              </div>
              <button class="bg-blue-500 text-white p-2 rounded-md" type="submit">Save</button>
              <button class="bg-red-500 text-white p-2 rounded-md" @click="showModal = false">Cancel</button>
            </form>
          </div>
        </div>
      </div>


      <div class="w-full max-w-2xl mx-auto shadow-lg rounded-xl border border-gray-200">
        <div class="p-3">
          <table class="table-auto w-full">
            <thead class="bg-white-800 text-gray-500">
              <tr>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-bold text-left">NAMA </div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-bold text-left">EMAIL </div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-bold text-left">UMUR </div>
                </th>
                <th class="p-2 whitespace-nowrap">
                  <div class="font-bold text-left">AKSI </div>
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="user in users" :key="user.id">
                <td class="text-gray-400 font-bold"> {{ user.nama }}</td>
                <td class="text-gray-400  font-bold">{{ user.email }}</td>
                <td class="text-gray-400  font-bold">{{ user.umur }}</td>
                <td>
                  <div>
                    <button class="text-gray-400 hover:text-gray-100  mr-2" @click="selectUser(user)">
                      <a class="text-gray-400 hover:text-gray-100 mx-3 ">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                          stroke="currentColor" class="w-6 h-6">
                          <path
                            d="M16.862 4.487l1.687-1.688a1.875 1.875 0 112.652 2.652L10.582 16.07a4.5 4.5 0 01-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 011.13-1.897l8.932-8.931zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0115.75 21H5.25A2.25 2.25 0 013 18.75V8.25A2.25 2.25 0 015.25 6H10" />
                        </svg>
                      </a>
                    </button>
                    <button class="material-icons-outlined text-base" @click="deleteUser(user.id)">
                      <a class="text-gray-400 hover:text-gray-100  mx-2">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                          stroke="currentColor" class="w-6 h-6">
                          <path
                            d="M22 10.5h-6m-2.25-4.125a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zM4 19.235v-.11a6.375 6.375 0 0112.75 0v.109A12.318 12.318 0 0110.374 21c-2.331 0-4.512-.645-6.374-1.766z" />
                        </svg>

                      </a>
                    </button>
                    <button class="" @click="showModal = true">
                      <a class="text-gray-400 hover:text-gray-100  mx-2">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                          stroke="currentColor" class="w-6 h-6">
                          <path
                            d="M19 7.5v3m0 0v3m0-3h3m-3 0h-3m-2.25-4.125a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zM4 19.235v-.11a6.375 6.375 0 0112.75 0v.109A12.318 12.318 0 0110.374 21c-2.331 0-4.512-.645-6.374-1.766z" />
                        </svg>

                      </a>
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>

          </table>
          <form v-if="selectedUser" @submit.prevent="updateUser(selectedUser.id)">
            <input v-model="selectedUser.nama" placeholder="Name">
            <input v-model="selectedUser.email" placeholder="Email">
            <input v-model="selectedUser.umur" placeholder="Age">
            <button
              type="submit">Save</button>
          </form>

        </div>
      </div>

    </div>

  </body>

  </html>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      showModal: false,
      nama: '',
      email: '',
      umur: '',
      users: [],
      selectedUser: null
    }
  },
  created() {
    this.getUsers();
    this.showModal = false
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
html,
body {
  margin: 0px;
  height: 100%;
}

#app {
  margin: 0px;
  height: 100%;
  font-weight: normal;
  --tw-bg-opacity: 1;
  background-color: rgb(17 24 39 / var(--tw-bg-opacity));
  height: 100%;
}
</style>