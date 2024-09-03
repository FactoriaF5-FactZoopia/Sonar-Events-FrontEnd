<script setup>
import { ref } from "vue";

const isModalVisible = ref(false);

const selectedDescription = ref("");

function showDescription(description) {
  selectedDescription.value = description;
  isModalVisible.value = true;
}

function closeModal() {
  isModalVisible.value = false;
}
</script>

<template>
  <main>
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
            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
              style="width: 10%"
            >
              Guns N'Roses
            </th>
            <td class="px-6 py-4">30/05/2024 17:00:00</td>
            <td class="px-6 py-4">Oviedo</td>
            <td class="px-6 py-4">True</td>
            <td class="px-6 py-4">False</td>
            <td class="px-6 py-4">350</td>
            <td class="px-6 py-4">500</td>
            <td class="px-6 py-4">http://image.url</td>
            <td class="px-6 py-4 description">
              <button
                id="button"
                class="text-blue-500 underline"
                @click="
                  showDescription(
                    'Es una de las bandas de rock más exitosas de todos los tiempos, habiendo vendido más de cien millones de discos, es considerada ícono global de la música y forma parte del prestigioso Salón de la Fama del Rock and Roll. Asimismo, la banda es uno de los números artísticos con más galardones, legado y repercusión mundial hasta la fecha. También Guns N\' Roses es considerada por muchos como una de las bandas más influyentes de la historia debido a su gran legado musical.'
                  )
                "
              >
                Show
              </button>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/edit.png" alt="" />
              </div>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/delete.png" alt="" />
              </div>
            </td>
          </tr>
          <tr
            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700"
            style="background-color: #d6d6d6"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
              style="width: 10%"
            >
              Guns N'Roses
            </th>
            <td class="px-6 py-4">30/05/2024 17:00:00</td>
            <td class="px-6 py-4">Oviedo</td>
            <td class="px-6 py-4">True</td>
            <td class="px-6 py-4">False</td>
            <td class="px-6 py-4">350</td>
            <td class="px-6 py-4">500</td>
            <td class="px-6 py-4">http://image.url</td>
            <td class="px-6 py-4 description">
              <button
                id="button"
                class="text-blue-500 underline"
                @click="
                  showDescription(
                    'Es una de las bandas de rock más exitosas de todos los tiempos, habiendo vendido más de cien millones de discos.'
                  )
                "
              >
                Show
              </button>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/edit.png" alt="" />
              </div>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/delete.png" alt="" />
              </div>
            </td>
          </tr>
          <tr
            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
              style="width: 10%"
            >
              Guns N'Roses
            </th>
            <td class="px-6 py-4">30/05/2024 17:00:00</td>
            <td class="px-6 py-4">Oviedo</td>
            <td class="px-6 py-4">True</td>
            <td class="px-6 py-4">False</td>
            <td class="px-6 py-4">350</td>
            <td class="px-6 py-4">500</td>
            <td class="px-6 py-4">http://image.url</td>
            <td class="px-6 py-4 description">
              <button
                id="button"
                class="text-blue-500 underline"
                @click="
                  showDescription(
                    'Es una de las bandas de rock más exitosas de todos los tiempos, habiendo vendido más de cien millones de discos, es considerada ícono global de la música y forma parte del prestigioso Salón de la Fama del Rock and Roll. Asimismo, la banda es uno de los números artísticos con más galardones, legado y repercusión mundial hasta la fecha. También Guns N\' Roses es considerada por muchos como una de las bandas más influyentes de la historia debido a su gran legado musical.'
                  )
                "
              >
                Show
              </button>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/edit.png" alt="" />
              </div>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/delete.png" alt="" />
              </div>
            </td>
          </tr>
          <tr
            class="odd:bg-white odd:dark:bg-gray-900 even:bg-gray-50 even:dark:bg-gray-800 border-b dark:border-gray-700"
            style="background-color: #d6d6d6"
          >
            <th
              scope="row"
              class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white"
              style="width: 10%"
            >
              Guns N'Roses
            </th>
            <td class="px-6 py-4">30/05/2024 17:00:00</td>
            <td class="px-6 py-4">Oviedo</td>
            <td class="px-6 py-4">True</td>
            <td class="px-6 py-4">False</td>
            <td class="px-6 py-4">350</td>
            <td class="px-6 py-4">500</td>
            <td class="px-6 py-4">http://image.url</td>
            <td class="px-6 py-4 description">
              <button
                id="button"
                class="text-blue-500 underline"
                @click="
                  showDescription(
                    'Es una de las bandas de rock más exitosas de todos los tiempos, habiendo vendido más de cien millones de discos, es considerada ícono global de la música y forma parte del prestigioso Salón de la Fama del Rock and Roll. Asimismo, la banda es uno de los números artísticos con más galardones, legado y repercusión mundial hasta la fecha. También Guns N\' Roses es considerada por muchos como una de las bandas más influyentes de la historia debido a su gran legado musical.'
                  )
                "
              >
                Show
              </button>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/edit.png" alt="" />
              </div>
            </td>
            <td class="px-6 py-4">
              <div id="containerEdit">
                <img id="icons" src="../assets/icons/delete.png" alt="" />
              </div>
            </td>
          </tr>
          <!-- Añade más filas aquí -->
        </tbody>
      </table>
    </div>

    <!-- Modal -->

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
  </main>
</template>

<style scoped>
main {
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
}

.modal-content {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  width: 90%;
  max-width: 600px;
  margin: 20px;
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
}
</style>
