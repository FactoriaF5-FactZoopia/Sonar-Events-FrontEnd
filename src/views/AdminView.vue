<template>
  <div>
    <h1></h1>

    <AddButton />

    <Table :events="events" @edit-event="handleEditEvent" @delete-event="handleDeleteEvent" />
  </div>
</template>

<script>
import Table from '../components/Table.vue';
import AddButton from '../components/AddButton.vue';

export default {
  name: 'AdminView',
  components: {
    Table,
    AddButton,
  },
  data() {
    return {
      events: [
        { id: 1, title: 'Estopa', date: '19 Oct 2024', available: 'Yes', pastEvent: 'No', maxParticipants: '7,500', location: 'Gijón', description: 'Plaza de Toros El Bibio', image: '' },
        { id: 2, title: 'The Hardkiss', date: '26 Oct 2024', available: 'Yes', pastEvent: 'No', maxParticipants: '1,100', location: 'Gijón', description: 'Patioh de la Laboral', image: '' },
        { id: 3, title: 'Nach', date: '31 Oct 2024', available: 'Yes', pastEvent: 'No', maxParticipants: '500', location: 'Oviedo', description: 'Sir Lauren\'s', image: '' }
      ]
    };
  },
  methods: {
    handleEditEvent(id) {
      console.log(`Editar evento con ID: ${id}`);
    },
    handleDeleteEvent(id) {
      console.log(`Eliminar evento con ID: ${id}`);
    }
  }
};
</script>
