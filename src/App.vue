<template>
  <div id="app">
    <div class="container">
      <h1>Yoqilg'i Darajasi Boshqaruvi</h1>

      <div v-for="(tank, index) in tanks" :key="index" class="tank-info">
        <h3>Bak {{ index + 1 }}</h3>
        <p>Joriy daraja: {{ tank.level }}%</p>
        <progress :value="tank.level" max="100"></progress>
        <div class="controls">
          <button class="btn" @click="decreaseLevel(index)">Darajani kamaytirish</button>
          <button class="btn" @click="increaseLevel(index)">Darajani oshirish</button>
        </div>

        <p v-if="tank.level < 10" class="warning">Ogohlantirish: Yoqilg'i darajasi juda past!</p>
      </div>

      <div v-if="alertMessage" class="alert">
        <p>{{ alertMessage }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // Barcha baklar uchun ma'lumot
      tanks: [
        { id: 1, level: 50 },
        { id: 2, level: 30 },
        { id: 3, level: 70 },
      ],
      alertMessage: "",
    };
  },
  methods: {
    decreaseLevel(index) {
      if (this.tanks[index].level > 0) {
        this.tanks[index].level -= 5;  // 5% kamaytirish
      }
      this.checkAlerts();  // Ogohlantirishlarni tekshirish
    },
    increaseLevel(index) {
      if (this.tanks[index].level < 100) {
        this.tanks[index].level += 5;  // 5% oshirish
      }
      this.checkAlerts();  // Ogohlantirishlarni tekshirish
    },
    checkAlerts() {
      this.alertMessage = "";  // Har safar yangilanishi uchun
      this.tanks.forEach(tank => {
        if (tank.level < 10) {
          this.alertMessage = "Ogohlantirish: Yoqilg'i darajasi past!";
        }
      });
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Arial', sans-serif;
  background-color: #f4f7fa;
  color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  width: 100%;
  max-width: 800px;
  background-color: white;
  margin: auto;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

h1 {
  font-size: 2rem;
  color: #5A5A5A;
  text-align: center;
  margin-bottom: 30px;
}

.tank-info {
  margin-bottom: 20px;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.tank-info h3 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

progress {
  width: 100%;
  height: 20px;
  border-radius: 10px;
  background-color: #e0e0e0;
}

.controls {
  margin-top: 10px;
}

.btn {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-right: 10px;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #45a049;
}

.warning {
  margin-top: 10px;
  color: red;
  font-weight: bold;
}

.alert {
  background-color: #fff3cd;
  color: #856404;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin-top: 20px;
}

@media (max-width: 600px) {
  .container {
    padding: 15px;
  }

  h1 {
    font-size: 1.5rem;
  }

  .tank-info {
    padding: 15px;
  }

  .btn {
    padding: 8px 16px;
    font-size: 0.9rem;
  }
}
</style>
