<script setup>
import { ref, onMounted } from "vue";

// Estado para el modal y eventos
const isModalVisible = ref(false);
const selectedDescription = ref("");
const events = ref([]);

const isCreateModalVisible = ref(false);
const isEditModalVisible = ref(false);

const newEvent = ref({
  title: "",
  date: "",
  place: "",
  available: true,
  past: false,
  registeredParticipants: 0,
  maxParticipants: 0,
  image: "",
  description: "",
});

const eventToEdit = ref(null);

// Funciones para manejar los modales
function showDescription(description) {
  selectedDescription.value = description;
  isModalVisible.value = true;
}

function closeModal() {
  isModalVisible.value = false;
}

function showCreateModal() {
  newEvent.value = {
    title: "",
    date: "",
    place: "",
    available: true,
    past: false,
    registeredParticipants: 0,
    maxParticipants: 0,
    image: "",
    description: "",
  };
  isCreateModalVisible.value = true;
}

function closeCreateModal() {
  isCreateModalVisible.value = false;
}

function showEditModal(event) {
  eventToEdit.value = { ...event };
  isEditModalVisible.value = true;
}

function closeEditModal() {
  isEditModalVisible.value = false;
}

// Función para obtener eventos
async function fetchEvents() {
  try {
    const response = await fetch(
      "http://localhost:8080/api/v1/events/allevents"
    );
    if (response.ok) {
      events.value = await response.json();
    } else {
      console.error("Error al obtener los eventos:", response.statusText);
    }
  } catch (error) {
    console.error("Error al conectar con el backend:", error);
  }
}

// Función para eliminar evento
async function deleteEvent(id) {
  try {
    const response = await fetch(`http://localhost:8080/api/v1/events/${id}`, {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
      },
    });

    if (response.ok) {
      events.value = events.value.filter((event) => event.id !== id);
      console.log("Evento eliminado con éxito");
    } else {
      console.error("Error al eliminar el evento:", response.statusText);
    }
  } catch (error) {
    console.error(
      "Error al conectar con el backend para eliminar el evento:",
      error
    );
  }
}

// Función para crear evento
async function createEvent() {
  try {
    const response = await fetch("http://localhost:8080/api/v1/events/create", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(newEvent.value),
    });

    if (response.ok) {
      const createdEvent = await response.json();
      events.value.push(createdEvent);
      closeCreateModal();
      console.log("Evento creado con éxito");
    } else {
      console.error("Error al crear el evento:", response.statusText);
    }
  } catch (error) {
    console.error(
      "Error al conectar con el backend para crear el evento:",
      error
    );
  }
}

// Función para actualizar evento
async function updateEvent() {
  try {
    const response = await fetch(
      `http://localhost:8080/api/v1/events/${eventToEdit.value.id}`,
      {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(eventToEdit.value),
      }
    );

    if (response.ok) {
      const updatedEvent = await response.json();
      const index = events.value.findIndex(
        (event) => event.id === updatedEvent.id
      );
      if (index !== -1) {
        events.value[index] = updatedEvent;
      }
      closeEditModal();
      console.log("Evento actualizado con éxito");
    } else {
      console.error("Error al actualizar el evento:", response.statusText);
    }
  } catch (error) {
    console.error(
      "Error al conectar con el backend para actualizar el evento:",
      error
    );
  }
}

// Función para manejar la carga de archivos en la creación
function handleFileUpload(event) {
  const file = event.target.files[0];
  if (file) {
    newEvent.value.image = file.name;
  }
}

// Función para manejar la carga de archivos en la edición
function handleFileUploadEdit(event) {
  const file = event.target.files[0];
  if (file) {
    eventToEdit.value.image = file.name;
  }
}

// Obtener eventos al montar el componente
onMounted(fetchEvents);
</script>

<template>
  <main>
    <!-- Botón para crear un nuevo evento -->
    <div id="containerCreate">
      <button id="buttonCreate" @click="showCreateModal">Add Event</button>
    </div>

    <!-- Tabla de eventos -->
    <div id="containerTable">
      <div id="table" class="relative overflow-x-auto shadow-md sm:rounded-lg">
        <table
          class="w-full text-sm text-left rtl:text-right text-gray-500 dark:text-gray-400"
        >
          <thead style="background-color: #301f35; color: white">
            <tr>
              <th scope="col" class="px-6 py-3">Event Name</th>
              <th scope="col" class="px-6 py-3">Date</th>
              <th scope="col" class="px-6 py-3">Place</th>
              <th scope="col" class="px-6 py-3">Available</th>
              <th scope="col" class="px-6 py-3">Past</th>
              <th scope="col" class="px-6 py-3">Participants</th>
              <th scope="col" class="px-6 py-3">Max Participants</th>
              <th scope="col" class="px-6 py-3">Image</th>
              <th scope="col" class="px-6 py-3">Description</th>
              <th scope="col" class="px-6 py-3">Edit</th>
              <th scope="col" class="px-6 py-3">Delete</th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="event in events"
              :key="event.id"
              class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b"
            >
              <th
                scope="row"
                class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
                style="width: 10%"
              >
                {{ event.title }}
              </th>
              <td class="px-6 py-4">{{ event.date }}</td>
              <td class="px-6 py-4">{{ event.place }}</td>
              <td class="px-6 py-4">{{ event.available ? "Yes" : "No" }}</td>
              <td class="px-6 py-4">{{ event.past ? "Yes" : "No" }}</td>
              <td class="px-6 py-4">{{ event.registeredParticipants }}</td>
              <td class="px-6 py-4">{{ event.maxParticipants }}</td>
              <td class="px-6 py-4">{{ event.image }}</td>
              <td class="px-6 py-4 description">
                <button
                  id="button"
                  class="text-blue-500 underline"
                  @click="showDescription(event.description)"
                >
                  Show
                </button>
              </td>
              <td class="px-6 py-4">
                <div id="containerEdit">
                  <img
                    id="icons"
                    src="../assets/icons/edit.png"
                    alt="Edit"
                    @click="showEditModal(event)"
                  />
                </div>
              </td>
              <td class="px-6 py-4">
                <div id="containerEdit">
                  <img
                    id="icons"
                    src="../assets/icons/delete.png"
                    alt="Delete"
                    @click="deleteEvent(event.id)"
                  />
                </div>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- Modal de descripción -->
    <div
      v-if="isModalVisible"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
      id="modal"
    >
      <div class="bg-white p-6 rounded-lg w-3/4 max-w-2xl">
        <h2 class="text-xl font-bold mb-4" style="text-align: center">
          Description
        </h2>
        <p class="mb-4">{{ selectedDescription }}</p>
        <div id="containerClose">
          <button
            id="close"
            @click="closeModal"
            class="bg-red-500 text-white px-4 py-2 rounded"
          >
            Close
          </button>
        </div>
      </div>
    </div>

    <!-- Modal de creación -->
    <div
      v-if="isCreateModalVisible"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
      id="create-modal"
    >
      <div class="bg-white p-6 rounded-lg w-3/4 max-w-2xl">
        <div id="containerTitle">
          <div id="containerTextEvent">
            <h2>Create New Event</h2>
          </div>
        </div>
        <form @submit.prevent="createEvent">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Title</label>
            <input
              v-model="newEvent.title"
              class="w-full p-2 border border-gray-300 rounded"
              type="text"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Date</label>
            <input
              v-model="newEvent.date"
              class="w-full p-2 border border-gray-300 rounded"
              type="datetime-local"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Place</label>
            <input
              v-model="newEvent.place"
              class="w-full p-2 border border-gray-300 rounded"
              type="text"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Available</label>
            <select
              v-model="eventToEdit.available"
              class="w-full p-2 border border-gray-300 rounded"
              id="available-edit"
            >
              <option value="true">Yes</option>
              <option value="false">No</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Past</label>
            <select
              v-model="eventToEdit.past"
              class="w-full p-2 border border-gray-300 rounded"
              id="past-edit"
            >
              <option value="true">Yes</option>
              <option value="false">No</option>
            </select>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1"
              >Registered Participants</label
            >
            <input
              v-model.number="newEvent.registeredParticipants"
              class="w-full p-2 border border-gray-300 rounded"
              type="number"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1"
              >Max Participants</label
            >
            <input
              v-model.number="newEvent.maxParticipants"
              class="w-full p-2 border border-gray-300 rounded"
              type="number"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Image</label>
            <input
              @change="handleFileUpload"
              id="image"
              class="w-full p-2 border border-gray-300 rounded"
              type="file"
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Description</label>
            <textarea
              v-model="newEvent.description"
              class="w-full p-2 border border-gray-300 rounded"
              rows="4"
              required
            ></textarea>
          </div>
          <div id="containerCreate">
            <button
              id="create"
              type="submit"
              class="text-white px-4 py-2 rounded"
            >
              Create
            </button>
            <button
              id="cancel"
              @click="closeCreateModal"
              class="text-white px-4 py-2 rounded ml-2"
            >
              Cancel
            </button>
          </div>
        </form>
      </div>
    </div>

    <!-- Modal de edición -->
    <div
      v-if="isEditModalVisible"
      class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
      id="edit-modal"
    >
      <div class="bg-white p-6 rounded-lg w-3/4 max-w-2xl">
        <div id="containerTitle">
          <div id="containerTextEvent">
            <h2>Edit Event</h2>
          </div>
        </div>
        <form @submit.prevent="updateEvent">
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Title</label>
            <input
              v-model="eventToEdit.title"
              class="w-full p-2 border border-gray-300 rounded"
              type="text"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Date</label>
            <input
              v-model="eventToEdit.date"
              class="w-full p-2 border border-gray-300 rounded"
              type="datetime-local"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Place</label>
            <input
              v-model="eventToEdit.place"
              class="w-full p-2 border border-gray-300 rounded"
              type="text"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Available</label>
            <select
              v-model="eventToEdit.available"
              class="w-full p-2 border border-gray-300 rounded"
              id="available-edit"
            >
              <option value="true">Yes</option>
              <option value="false">No</option>
            </select>
          </div>

          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Past</label>
            <select
              v-model="eventToEdit.past"
              class="w-full p-2 border border-gray-300 rounded"
              id="past-edit"
            >
              <option value="true">Yes</option>
              <option value="false">No</option>
            </select>
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1"
              >Registered Participants</label
            >
            <input
              v-model.number="eventToEdit.registeredParticipants"
              class="w-full p-2 border border-gray-300 rounded"
              type="number"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1"
              >Max Participants</label
            >
            <input
              v-model.number="eventToEdit.maxParticipants"
              class="w-full p-2 border border-gray-300 rounded"
              type="number"
              required
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Image</label>
            <input
              @change="handleFileUploadEdit"
              id="image"
              class="w-full p-2 border border-gray-300 rounded"
              type="file"
            />
          </div>
          <div class="mb-4">
            <label class="block text-sm font-medium mb-1">Description</label>
            <textarea
              v-model="eventToEdit.description"
              class="w-full p-2 border border-gray-300 rounded"
              rows="4"
              required
            ></textarea>
          </div>
          <div id="containerCreate">
            <button
              id="update"
              type="submit"
              class="text-white px-4 py-2 rounded"
            >
              Update
            </button>
            <button
              id="cancel"
              @click="closeEditModal"
              class="text-white px-4 py-2 rounded ml-2"
            >
              Cancel
            </button>
          </div>
        </form>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  min-height: 600px;
}
#containerCreate {
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
#buttonCreate {
  width: 70%;
  height: 50px;
  background-color: #301f35;
  color: white;
  border-radius: 10px;
  box-shadow: 0 5px 10px #d43089;
}
#buttonCreate:hover {
  background-color: #d43089;
  box-shadow: 0 5px 10px #301f35;
}
#containerTable {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 400px;
}
#table {
  width: 80%;
  box-shadow: 0 5px 10px #d43089;
}
tr,
thead {
  box-shadow: 0 3px 20px #d43089;
}
#containerEdit {
  width: 40px;
  height: 40px;
  background-color: #301f35;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

#icons {
  width: 75%;
}

#containerEdit:hover {
  background-color: #d43089;
}
#tdIcons {
  width: 8%;
}
.description {
  width: 10%;
}
#button {
  text-decoration: none;
  color: #301f35;
  font-weight: bold;
}
#containerClose {
  display: flex;
  justify-content: center;
  align-items: center;
}
#close {
  background-color: #301f35;
}
#modal {
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  width: 90%;
  max-width: 600px;
  margin: 20px;
}
#containerTextEvent {
  width: 70%;
  height: 40px;
  background-color: #301f35;
  color: white;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
}
#containerTitle {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 25px;
}
label {
  color: #301f35;
  font-weight: bold;
}
input {
  height: 30px;
}
#available {
  height: 30px;
  font-size: 10px;
}
#pastEvent {
  height: 30px;
  font-size: 10px;
}
textarea {
  height: 70px;
}
#buttons {
  background-color: #301f35;
  margin: 10px;
}
#buttons:hover {
  background-color: #d43089;
}
.buttons {
  display: flex;
  justify-content: center;
  align-items: center;
}
#fileImage {
  height: 40px;
}
#create,
#cancel,
#update {
  background-color: #301f35;
}
#create:hover,
#cancel:hover,
#update:hover {
  background-color: #d43089;
}
#available-edit,
#past-edit {
  height: 35px;
  font-size: 14px;
}
#image {
  height: 40px;
}
@media (max-width: 768px) {
  #table {
    width: 85%;
    border-radius: 10px;
  }
  #modal {
    align-items: center;
    justify-content: center;
  }

  .modal-content {
    width: 95%;
    height: 100px;
  }
  #containerTitle {
    font-size: 14px;
  }
}
</style>
