<script setup>
import { reactive } from "vue";

const items = reactive([
    { title: "What is HTML?", content: "HTML is the short form of Hyper Text Markup Language", open: false },
    { title: "What is CSS?", content: "CSS is the short form of Cascading Style Sheet.", open: false },
    { title: "What is JS?", content: "JS is the short form of Java Script. It makes the website more interactive.", open: false }
]);

const toggleAccordion = (index) => {
    items.forEach((item, i) => {
        item.open = i === index ? !item.open : false;
    });
};
</script>

<template>
    <div class="accordion-container">
        <div v-for="(item, index) in items" :key="item.title" class="accordion">
            <div class="accordion-header" @click="toggleAccordion(index)">
                <h2>{{ item.title }}</h2>
                <span class="arrow-icon">{{ item.open ? "&#129075;" : "&#129074;" }}</span>
            </div>
            <div v-if="item.open" class="accordion-content">
                <p>{{ item.content }}</p>
            </div>
        </div>
    </div>
</template>


<style scoped>
.accordion-container {
  width: 500px;
  margin: 50px auto;
  font-family: Arial, sans-serif;
}

.accordion {
  border: 1px solid #ddd;
  border-radius: 5px;
  margin-bottom: 10px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.accordion-header {
  background-color: #007bff;
  color: white;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  transition: background-color 0.3s;
}

.accordion-header:hover {
  background-color: #0056b3;
}

.accordion-header h2 {
  margin: 0;
  font-size: 18px;
}

.accordion-header .arrow-icon {
  font-size: 18px;
}

.accordion-content {
  padding: 15px;
  background-color: #f9f9f9;
  font-size: 16px;
  color: #333;
  border-top: 1px solid #ddd;
  line-height: 1.5;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
