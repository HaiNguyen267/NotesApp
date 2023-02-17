<template>
  <main>
    <div class="overlay" v-show="showModal">
      <div class="background" @click="closeModal"></div>
      <div class="modal-content">
        <textarea name="" id="" cols="30" rows="10" v-model.trim="newNote" @keyup.enter="addNote"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button class="add-note-btn" @click="addNote">Add note</button>

      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="openModal">+</button>
      </header>

      <div class="card-container">
        <div class="card" 
          v-for="(note, index) in allNotes" 
          :style="{ backgroundColor: note.backgroundColor }"
          :key="index">

          <p class="main-text">{{ note.content }}</p>
          <p class="date">{{ note.date }}</p>
        </div>

      </div>



    </div>
</main>
</template>

<script setup>
import { reactive, ref, computed } from 'vue';

const showModal = ref(false)
const newNote = ref('')
const allNotes = reactive([
])
const errorMessage = computed(() => {
  if (newNote.value.length < 5) {
    return "A note must be at least 5 characters long"
  } else {
    return ""
  }
})
function closeModal() {
  showModal.value = false
}

function openModal() {
  console.log('openModal is working');

  showModal.value = true
}

function generateRandomColor() {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

function addNote() {

  allNotes.push({
    content: newNote.value,
    date: new Date().toLocaleTimeString('en-GB'),
    backgroundColor: generateRandomColor()
  })

  closeModal()
  newNote.value = ''

}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@500&display=swap');

* {
  margin: 0;
  padding: 0;
}

main {
  font-family: 'Roboto', sans-serif;
  height: 100vh;
  width: 100vw;
}

.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
  color: white;
}

button {
  font-family: 'Roboto', sans-serif;
  border: none;
  cursor: pointer;
  width: 50px;
  height: 50px;
  background: rgb(200, 200, 200);
  border-radius: 50%;
  font-size: 25px;
  transition: all 0.2s ease-in-out;
}

button:hover {
  background: white;
}

.card {
  font-family: 'Roboto', sans-serif;
  width: 200px;
  height: 200px;
  background: lightblue;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 10px;
  margin: 0px 20px 20px 0px;
  color: black;
}

.date {
  font-size: 12px;
  font-weight: bold;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
}

.background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  /* semi-transparent black */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-content p {
  color: red;
}
.modal-content {
  width: 750px;
  height: 500px;
  background: white;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

textarea {
  font-family: 'Roboto', sans-serif;
  width: 85%;
  height: 70%;
  font-size: 20px;
  border-radius: 10px;
}

textarea:focus {
  outline: none;
}

.add-note-btn {
  margin-top: 20px;
  width: 150px;
  boder: none;
  border-radius: 10px;
}

.add-note-btn:hover {
  background: lightblue;
}
</style>