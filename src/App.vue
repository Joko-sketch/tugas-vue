<template>
  <div class="app-container">
    <!-- Click Counter Card -->
    <section class="card">
      <h2>Click Counter</h2>
      <button @click="incrementCounter" class="action-button">Click me</button>
      <button @click="resetCounter" class="action-button reset-button">Reset</button>
      <p class="counter-text">You've clicked the button <span>{{ counter }}</span> times.</p>
    </section>

    <!-- Box Color Changer Card -->
    <section class="card">
      <h2>Box Color Changer</h2>
      <div :style="{ backgroundColor: currentColor }" class="color-box"></div>
      <button @click="changeColor" class="action-button">Change Color</button>
      <div class="color-palette">
        <h3>Available Colors</h3>
        <div v-for="color in colors" :key="color" 
             :style="{ backgroundColor: color }" 
             class="color-swatch"
             @click="setColor(color)">
        </div>
      </div>
    </section>

    <!-- Image Carousel Card -->
    <section class="card">
      <h2>Image Carousel</h2>
      <div class="carousel-container">
        <button @click="prevImage" class="carousel-button prev-button">❮</button>
        <img :src="images[currentImage]" alt="Image Carousel" class="carousel-image">
        <button @click="nextImage" class="carousel-button next-button">❯</button>
      </div>
    </section>
  </div>
</template>

<script>
import { ref, watch } from 'vue';
export default {
  setup() {
    const counter = ref(0);
    const incrementCounter = () => {
      counter.value++;
    };
    const resetCounter = () => {
      counter.value = 0;
    };
    const colors = ['#FF6347', '#3CB371', '#1E90FF', '#FFD700', '#8A2BE2', '#808080', '#FFC0CB', '#000000', '#A52A2A', '#f0f0f0'];
    const currentColor = ref(colors[0]);
    const changeColor = () => {
      const randomIndex = Math.floor(Math.random() * colors.length);
      currentColor.value = colors[randomIndex];
    };
    const setColor = (color) => {
      currentColor.value = color;
    };
    const images = [
      'https://i.pinimg.com/originals/a9/0c/37/a90c378d08fcac3514b79c852713f26e.jpg',
      'https://i.pinimg.com/originals/e4/3d/10/e43d10bd0d7a370f2eed68eb7791858f.jpg',
      'https://i.pinimg.com/736x/e4/ea/03/e4ea038a91f398f6b27e13c30b327372.jpg',
      'https://i.pinimg.com/originals/c6/a8/5b/c6a85bd2f517869e35ce0ece3ace8105.jpg',
      'https://i.pinimg.com/originals/bb/a4/cd/bba4cdc5ae553064d2fff8d1663a0582.jpg',
      'https://i.pinimg.com/originals/94/ae/fe/94aefebbb20286aedf467dea994fda32.jpg',
      'https://i.pinimg.com/originals/6b/c0/da/6bc0da6ef0a8a22d8a52cc22d89a718b.png',
      'https://i.pinimg.com/originals/84/5c/36/845c36e8095d610f1db41aa7e5481786.jpg',
      'https://i.pinimg.com/originals/52/24/3e/52243e3ab432432bf6cef3c965991fd8.jpg',
      'https://i.pinimg.com/originals/19/e8/0a/19e80a0f57bff379225006320d764c2d.jpg',
      'https://i.pinimg.com/originals/df/0c/3b/df0c3bd0be5d5697b7c44532cd2623bb.jpg'
    ];
    const currentImage = ref(0);
    const nextImage = () => {
      currentImage.value = (currentImage.value + 1) % images.length;
    };
    const prevImage = () => {
      currentImage.value = (currentImage.value - 1 + images.length) % images.length;
    };
    watch(currentColor, (newColor) => {
      document.body.style.backgroundColor = newColor;
    });
    return {
      counter,
      incrementCounter,
      resetCounter,
      currentColor,
      changeColor,
      setColor,
      colors,
      images,
      currentImage,
      nextImage,
      prevImage
    };
  }
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f5f5f5;
  transition: background-color 0.5s ease; 
}
.app-container {
  max-width: 800px;
  margin: 20px auto;
  padding: 20px;
}
.card {
  background-color: #ffffff;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 20px;
  text-align: center;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1), 
              0 4px 6px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  opacity: 0; 
}
.card:hover {
  transform: translateY(-5px); 
  box-shadow: 0 15px 25px rgba(0, 0, 0, 0.15), 
              0 8px 10px rgba(0, 0, 0, 0.05);
}
.card:nth-child(1) {
  transform: translateX(-100%); 
  animation: slide-in-right 0.8s ease forwards 0.2s; 
}
.card:nth-child(2) {
  transform: translateX(-100%); 
  animation: slide-in-left 0.8s ease forwards 0.4s; 
}
.card:nth-child(3) {
  transform: translateX(-100%); 
  animation: slide-in-right 0.8s ease forwards 0.6s; 
}
@keyframes slide-in-right {
  0% {
    opacity: 0;
    transform: translateX(100%); 
  }
  100% {
    opacity: 1;
    transform: translateX(0); 
  }
}
@keyframes slide-in-left {
  0% {
    opacity: 0;
    transform: translateX(-100%); 
  }
  100% {
    opacity: 1;
    transform: translateX(0); 
  }
}
.action-button {
  background-color: #007BFF;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
  margin: 5px;
}
.action-button:hover {
  background-color: #0056b3;
}
.reset-button {
  background-color: #dc3545;
}
.reset-button:hover {
  background-color: #c82333;
}
.counter-text span {
  font-weight: bold;
}
.color-box {
  transition: background-color 0.5s;
  width: 150px;
  height: 150px;
  margin: 10px auto;
  border-radius: 8px;
}
.color-palette {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  margin-top: 10px;
}
.color-swatch {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  transition: transform 0.2s;
}
.color-swatch:hover {
  transform: scale(1.1);
}
.carousel-container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.carousel-image {
  width: 100%;
  max-height: 300px;
  object-fit: cover;
  border-radius: 8px;
  transition: opacity 0.5s ease-in-out;
}
.carousel-button {
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  padding: 10px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 24px;
  transition: background-color 0.3s;
}
.carousel-button:hover {
  background-color: rgba(0, 0, 0, 0.8);
}
.prev-button {
  margin-right: 10px;
}
.next-button {
  margin-left: 10px;
}
</style>
