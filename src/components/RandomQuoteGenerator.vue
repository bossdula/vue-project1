<script setup>
import { ref, onMounted } from "vue";

const quotes = ref([
    {
        text: "The only thing we have to fear is fear itself.",
        author: "Franklin D. Roosevelt"
    },
    {
        text: "That’s one small step for a man, one giant leap for mankind.",
        author: "Neil Armstrong"
    },
    {
        text: "I have no special talent. I am only passionately curious.",
        author: "Albert Einstein"
    },
    {
        text: "An eye for an eye will leave the whole world blind.",
        author: "Mahatma Gandhi"
    },
    {
        text: "The journey of a thousand miles begins with one step.",
        author: "Lao Tzu"
    }
]);

const currentQuote = ref({text:"", author:""});

const getRandomQuote = () => {
    const randomIndex = Math.floor(Math.random() * quotes.value.length);
    currentQuote.value = quotes.value[randomIndex];
}

onMounted(getRandomQuote)
</script>


<template>
    <div class="quote-generator">
        <h2 class="app-title">Random Quote Generator</h2>
        <blockquote class="quote-container">
            <p class="quote-text">{{ currentQuote.text }}</p>
            <cite>{{ currentQuote.author }}</cite>
        </blockquote>

        <button @click="getRandomQuote" class="quote-button">Generate Random Quote</button>
    </div>
</template>

<style scope>
.quote-generator {
    max-width: 500px;
    margin: 40px auto;
    padding: 20px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
    border-radius: 10px;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.5)
}

.app-title {
    text-align: center;
    margin-bottom: 20px;
}

.quote-container {
    padding: 20px;
    background-color: #f7f7f7;
    border: 1px solid #ddd;
    border-radius: 10px;
    margin-bottom: 10px;
}

.quote-button {
    padding: 10px;
    background-color: #4CAF50;
    color: #fff;
    float: right;
    border: 1px solid #4CAF50;
    border-radius: 5px;
    cursor: pointer;
    font-size: 15px;
}

.quote-button:hover {
    background-color: #139117;
}

.quote-text {
    font-size: 18px;
    font-style: italic;
    margin-bottom: 8px;
}
</style>