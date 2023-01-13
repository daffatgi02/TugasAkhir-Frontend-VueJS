<form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" @submit.prevent="createUser">
    <div >
      <label >Nama: </label>
      <input v-model="nama"
         />
    </div>
    <div >
      <label >Email: </label>
      <input v-model="email"
         />
    </div>
    <div >
      <label >Umur: </label>
      <input v-model="umur"
         />
    </div>
    <button
      
      type="submit">Save</button>
  </form>