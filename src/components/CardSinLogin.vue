<script setup>
import { ref, onMounted } from 'vue';

const events = ref([]);
const showModal = ref(false);
const selectedEvent = ref(null);
const isBackgroundChanged = ref(false);
const assistText = ref("Reserve a Place");


const fetchEvents = async () => {
  try {
    const response = await fetch('http://localhost:8080/api/v1/events/allevents');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log('Fetched events:', data);
    events.value = data.map(event => ({
      id: event.id,
      title: event.title,
      date: new Date(event.date).toLocaleString(), 
      location: event.place,
      currentAttendees: event.registeredParticipants,
      totalAttendees: event.maxParticipants,
      description: event.description,
      imageUrl: event.image,
      isAvailable: event.available,
      isPast: event.past,
    }));
  } catch (error) {
    console.error('Error fetching events:', error);
  }
};

const toggleBackgroundColorAndText = () => {
  isBackgroundChanged.value = !isBackgroundChanged.value;
  assistText.value = isBackgroundChanged.value ? "Confirmed Attendance" : "Reserve a Place";
};


const showEventDetails = (event) => {
  selectedEvent.value = event;
  console.log('Selected event:', event); // Depuración: Verifica el evento seleccionado
  showModal.value = true;
};

onMounted(fetchEvents);
</script>

<template>
  <div class="container">
    <div v-for="event in events" :key="event.id" class="item-container">
      <div class="img-container">
        <img id="img" :src="event.imageUrl" alt="Event image" />
      </div>

      <div class="body-container">
        <div class="overlay"></div>

        <div class="event-info">
          <p class="title">{{ event.title }}</p>
          <div class="separator"></div>
          <p class="info">
            <i class="far fa-calendar-alt"></i>
            {{ event.date }}
          </p>
          <p class="price">
            <i id="iconUser" class="fa fa-user-circle"></i>
            <span>{{ event.currentAttendees }}</span>
            <span>/</span>
            <span>{{ event.totalAttendees }}</span>
          </p>

          <div class="additional-info">
            <p class="info">
              <i class="fas fa-map-marker-alt"></i>
              {{ event.location }}
            </p>

            <p class="info">
              <div 
                id="checked" 
                :class="{ 'background-changed': isBackgroundChanged }" 
              >
                {{ assistText }}
              </div>
            </p>

            <p class="info description" @click="showEventDetails(event)">
              <i class="fas fa-info-circle"></i>
              <span>Description</span>
            </p>
          </div>
        </div>
        <button class="action" @click="toggleBackgroundColorAndText">Book it</button>
      </div>
    </div>

    <!-- Modal -->
    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <span class="close" @click="showModal = false">&times;</span>
        <p>{{ selectedEvent?.description || 'No description available' }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}

.item-container {
  position: relative;
  margin: 28px;
  width: 320px;
  height: 580px;
  overflow: hidden;
  background-color: #fff;
  box-shadow: 0 0 15px 15px#301f35;
  cursor: pointer;
  border-radius: 8px;
}
.item-container:hover {
  box-shadow: 0 0 20px 15px#d43089;
}

.img-container,
.body-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 400px;
}
#img {
  height: 400px;
  object-fit: cover;
}

.img-container img {
  width: 100%;
}

.body-container {
  position: relative;
}

.overlay {
  position: relative;
  width: 100%;
  height: 400px;
  background-color: rgba(24, 83, 122, 0.6);
  opacity: 0;
  transition: height linear 0.4s, opacity linear 0.2s;
}

.item-container:hover .overlay {
  opacity: 1;
  height: 220px;
}

.event-info {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 8px;
}

.title,
.price {
  color: #301f35;
  font-size: 1.5em;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 12px;
}

.info {
  letter-spacing: 0.5px;
  margin-bottom: 6px;
}

.separator {
  width: 80%;
  height: 6px;
  background-color: #301f35;
  margin-bottom: 16px;
}

.additional-info {
  border-top: 1px solid #bbb;
  margin-top: 12px;
  padding: 28px;
  padding-bottom: 0;
}

.additional-info .info {
  font-size: 0.9em;
  margin-bottom: 20px;
  text-align: center;
}

.info i {
  color: #301f35;
  font-size: 1.1em;
  margin-right: 4px;
}

.info span {
  color: #301f35;
  font-weight: bolder;
}
#iconUser {
  margin: 5px;
}
.action {
  color: #fff;
  border: 3px solid #fff;
  background-color: #301f35;
  position: absolute;
  top: -100px;
  left: 50%;
  transform: translateX(-50%);
  width: 60%;
  outline: none;
  cursor: pointer;
  padding: 12px;
  text-transform: uppercase;
  font-size: 1.3em;
  font-weight: bold;
  letter-spacing: 2px;
  transition: background-color 0.4s, top 0.4s;
}

.item-container:hover .action {
  top: 80px;
}

.action:hover {
  background-color: #d43089;
}
#link {
  font-weight: bold;
}
/* Modal styles */
.modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  z-index: 1000;
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 500px;
  text-align: center;
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 20px;
  font-size: 24px;
  font-weight: bold;
  cursor: pointer;
}
#checked{
  width: 170px;
  height: 30px;
 
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 3px solid #301f35;
}

.background-changed {
  background-color: #301f35; 
  color: white;
}
</style>
