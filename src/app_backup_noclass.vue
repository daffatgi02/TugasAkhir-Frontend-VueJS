<template>


    <!-- DIV KESELURUHAN -->
    <div class="">
      <!-- TABLE MENAMPILKAN DATA -->
      <table class="">
        <thead>
          <tr>
            <th class="">ID</th>
            <th class="">Nama</th>
            <th class="">Email</th>
            <th class="">Umur</th>
            <th class="">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td class="">{{ user.id }}</td>
            <td class="">{{ user.nama }}</td>
            <td class="">{{ user.email }}</td>
            <td class="">{{ user.umur }}</td>
            <td class="">
              <button
                class=""
                @click="selectUser(user)">Select</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- -----END---- -->
  
    <!-- TABLE CREATE -->
    <div class="">
      <div class="">
        <table class="">
          <thead class="">
            <th scope="col" class="">
              <tr>
                <td>Nama: </td>
                <td>
                  <input
                    class=""
                    type="text" id="nama" v-model="nama" />
                </td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <td>Email:</td>
                <td>
                  <input
                    class=""
                    type="email" id="email" v-model="email" />
                </td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <td>Umur:</td>
                <td>
                  <input
                    class=""
                    type="number" id="number" v-model="umur" />
                </td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <td colspan="2">
                  <button
                    class=""
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
    <div class="">
      <div>
        <table v-if="selectedUser"
          class="">
          <thead class="">
            <th scope="col" class="">
              <tr>
                <th for="nama"> Nama: </th>
                <td><input
                    class=""
                    type="text" id="nama" v-model="selectedUser.nama" /></td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <th for="email"> Email: </th>
                <td><input
                    class=""
                    type="email" id="email" v-model="selectedUser.email" /></td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <th for="email"> Umur: </th>
                <td><input
                    class=""
                    type="number" id="number" v-model="selectedUser.umur" /></td>
              </tr>
            </th>
            <th scope="col" class="">
              <tr>
                <td>
                  <button
                    class=""
                    type="submit" @click="updateUser(selectedUser.id)">Update User</button>
                </td>
                <td>
                  <button
                    class=""
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
  