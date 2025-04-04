<template>
  <div class="city-time-viewer">
    <h1>World Time Viewer</h1>
    
    <form @submit.prevent="fetchTime">
      <input
        type="text"
        v-model="city"
        placeholder="Enter a city name"
      />
      <button type="submit" :disabled="isLoading">
        {{ isLoading ? 'Loading...' : 'Get Time' }}
      </button>
    </form>
    
    <div v-if="error" class="error">{{ error }}</div>
    
    <div v-if="timeData" class="time-display">
      <h2>{{ timeData.city }}</h2>
      <div class="time">{{ timeData.formatted }}</div>
      <div class="timezone">Timezone: {{ timeData.timezone }}</div>
    </div>
    
    <div v-if="recentCities.length > 0" class="recent-cities">
      <h3>Recent Cities:</h3>
      <ul>
        <li v-for="(recentCity, index) in recentCities" :key="index">
          <button @click="setCityAndFetch(recentCity)">
            {{ recentCity }}
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: '',
      timeData: null,
      error: '',
      isLoading: false,
      recentCities: []
    };
  },
  methods: {
    async fetchTime() {
      if (!this.city.trim()) return;
      
      this.isLoading = true;
      this.error = '';
      
      try {
        const response = await axios.get(
          'https://time-viewer-backend.vercel.app/api/time',
          { params: { city: this.city } }
        );
        this.timeData = response.data;
        this.addToRecentCities(this.city);
      } catch (err) {
        this.error = err.response?.data?.error || 'Failed to fetch time';
        this.timeData = null;
      } finally {
        this.isLoading = false;
      }
    },
    addToRecentCities(city) {
      this.recentCities = [
        city,
        ...this.recentCities.filter(c => c !== city)
      ].slice(0, 5);
    },
    setCityAndFetch(city) {
      this.city = city;
      this.fetchTime();
    }
  }
};
</script>

<style scoped>
/* Copy the same CSS from your React version (App.css) */
.city-time-viewer {
  margin-top: 50px;
}

h1{
  color:aqua;
}

input {
  padding: 10px;
  font-size: 16px;
  width: 300px;
  margin-right: 10px;
}
button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}
.error {
  color: red;
}
.time-display {
  margin-top: 30px;
}
.time {
  font-size: 48px;
  font-weight: bold;
}
</style>