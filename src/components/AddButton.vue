<template>
  <div class="add-button-container">
    <button @click="showModal = true">Add Event</button>

    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <span class="close" @click="showModal = false">&times;</span>
        <h2>Add New Event</h2>
        <form>
          <label for="title">Title:</label>
          <input type="text" id="title" />

          <label for="date">Date:</label>
          <!-- <input type="date" id="date" /> -->
          <input type="datetime-local" />

          <label for="date">Place:</label>
          <input type="text" id="place" />
          <label for="available">Available:</label>
          <select id="available">
            <option value="Yes">Yes</option>
            <option value="No">No</option>
          </select>

          <label for="pastEvent">Past Event:</label>
          <select id="pastEvent">
            <option value="Yes">Yes</option>
            <option value="No">No</option>
          </select>

          <label for="maxParticipants">Actual Participants:</label>
          <input type="number" id="actualParticipants" />

          <label for="maxParticipants">Max Participants:</label>
          <input type="number" id="maxParticipants" />

          <label for="image">Image:</label>
          <input type="file" id="image" />

          <label for="description">Description:</label>
          <textarea id="description"></textarea>

          <button type="button" @click="showModal = false">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
</script>

<style scoped>
.add-button-container {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
  padding: 0 10px;
}

button {
  background-color: #d43089;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  width: 80%;
  max-width: 1200px;
  box-sizing: border-box;
  font-size: 16px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #a31c62;
}

@media (max-width: 768px) {
  button {
    font-size: 14px;
    padding: 8px 15px;
  }
}

.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  width: 400px;
  max-width: 90%;
}

.close {
  float: right;
  font-size: 24px;
  font-weight: bold;
  cursor: pointer;
}

label {
  display: block;
  margin-top: 10px;
}

input,
textarea,
select {
  width: 100%;
  padding: 8px;
  margin-top: 5px;
  box-sizing: border-box;
}
</style>
