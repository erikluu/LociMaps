<script setup>
import { ref, onMounted } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import { fas } from '@fortawesome/free-solid-svg-icons'

let input = ref("");
let placeholderText = ref("Press [/] to search");

function clearPlaceholder() {
    placeholderText.value = "";
}

function restorePlaceholder() {
    placeholderText.value = "Press [/] to search";
}

onMounted(() => {
    document.addEventListener('keydown', handleKeyDown);
});

function handleKeyDown(event) {
    if (event.key === '/') {
        event.preventDefault();
        const searchInput = document.querySelector('input[type="text"]');
        searchInput.focus();
    } else if (event.key === 'Escape') {
        const searchInput = document.querySelector('input[type="text"]');
        searchInput.blur();
    }
}

</script>

<template>
    <input type="text" v-model="input" :placeholder=placeholderText @focus="clearPlaceholder" @blur="restorePlaceholder"/>
</template>

<style scoped>
input[type="text"] {
    padding: 10px;
    border-radius: 5px;
        
    position: absolute;
    top: 0;
    right: 0;
    margin: 1em;
    width: min(180px, 80%);
    transition: width 0.3s ease;
    z-index: 1;
}

input[type="text"]:focus {
    width: min(calc(10% + 10%), 90%);
}
</style>
