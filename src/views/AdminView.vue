<script>
import Table from '../components/Table.vue';

export default {
  name: 'AdminView',
  components: {
    Table,
  },
};
</script>

<template>
  <div>
    <h1>Admin View</h1>

    <Table />
  </div>
</template>

<style scoped>
main {
  height: 800px;
}
</style>