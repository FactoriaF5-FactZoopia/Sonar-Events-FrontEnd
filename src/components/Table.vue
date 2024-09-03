<template>
  <div class="table-container">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Title</th>
          <th scope="col">Date</th>
          <th scope="col">Available</th>
          <th scope="col">Past Event</th>
          <th scope="col">Max Participants</th>
          <th scope="col">Location</th>
          <th scope="col">Description</th>
          <th scope="col">Image</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="event in events" :key="event.id">
          <th scope="row">{{ event.id }}</th>
          <td>{{ event.title }}</td>
          <td>{{ event.date }}</td>
          <td>{{ event.available }}</td>
          <td>{{ event.pastEvent }}</td>
          <td>{{ event.maxParticipants }}</td>
          <td>{{ event.location }}</td>
          <td>{{ event.description }}</td>
          <td>{{ event.image }}</td>
          <td>
            <button @click="editEvent(event.id)"><EditIcon /></button>
          </td>
          <td>
            <button @click="deleteEvent(event.id)"><TrashIcon /></button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import EditIcon from '../assets/icons/EditIcon.vue';
import TrashIcon from '../assets/icons/TrashIcon.vue';

export default {
  name: 'TableComponent',
  props: {
    events: {
      type: Array,
      required: true
    }
  },
  components: {
    EditIcon,
    TrashIcon
  },
  methods: {
    editEvent(id) {
      this.$emit('edit-event', id);
    },
    deleteEvent(id) {
      this.$emit('delete-event', id);
    }
  }
}
</script>

  
  <style scoped>
  .table-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    padding: 10px;
    box-sizing: border-box;
  }
  
  table {
    width: 100%;
    max-width: 1200px;
    border-collapse: collapse;
  }
  
  td, th {
    padding: 10px;
    border: 1px solid #ddd;
    text-align: center;
  }
  
  table th {
    background-color: #d43089;
  }
  
  table tbody tr:nth-child(odd) {
    background-color: #ffffff;
  }
  
  table tbody tr:nth-child(even) {
    background-color: #f9f9f9;
  }
  
  table tbody tr:hover {
    background-color: #f1f1f1;
  }
  
  button {
    padding: 10px 15px;
    background-color: #d43089;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    height: 70px;
    width: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  button:hover {
    background-color: #a31c62;
  }
  
  button svg {
    width: 24px;
    height: 24px;
  }
  
  @media (max-width: 600px) {
    table {
      font-size: 12px;
    }
  
    button {
      padding: 8px 12px;
    }
  }
  </style>
  