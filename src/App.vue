<template>
  <div class="app">
    <h1>Daftar Kegiatan</h1>

    <!-- Form untuk menambahkan kegiatan -->
<form @submit.prevent="addActivity">
  <input type="text" v-model="newActivity" placeholder="Tambahkan kegiatan baru">
  
  <button type="submit" style="margin-right: 10px;">Tambah</button> <!-- Tambahkan margin-right di sini -->
</form>


    <!-- Kotak untuk menyimpan filter -->
    <div class="filter-box">
      <!-- Filter untuk menampilkan semua kegiatan -->
      <button @click="showAll">Semua</button>

      <!-- Filter untuk menampilkan kegiatan yang belum selesai -->
      <button @click="showPending">Belum Selesai</button>

      <!-- Filter untuk menampilkan kegiatan yang sudah selesai -->
      <button @click="showCompleted">Selesai</button>
    </div>

    <!-- Daftar kegiatan -->
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <input type="checkbox" v-model="activity.completed">
        <span :class="{ 'completed': activity.completed }">{{ activity.name }}</span>
        <button @click="cancelActivity(index)">Batalkan</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [],
      showOnlyPending: false
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ name: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1);
    },
    showAll() {
      this.showOnlyPending = false;
    },
    showPending() {
      this.showOnlyPending = true;
    },
    showCompleted() {
      this.showOnlyPending = false;
    }
  },
  computed: {
    filteredActivities() {
      if (this.showOnlyPending) {
        return this.activities.filter(activity => !activity.completed);
      } else {
        return this.activities;
      }
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}

body {
  background-color: #f0f0f0; /* Warna latar belakang */
  font-family: Arial, sans-serif; /* Jenis huruf */
  margin: 0; /* Hilangkan margin default */
  padding: 0; /* Hilangkan padding default */
}

.app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;

}

h1 {
  margin-bottom: 20px;
}

form {
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 10px;
}

button {
  margin-right: 10px;
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background-color: #4caf50;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

input[type="checkbox"] {
  margin-right: 5px;
}

.completed {
  text-decoration: line-through;
}

.filter-box {
  margin-bottom: 20px;
}

.filter-box button {
  margin-right: 10px;
}

</style>
