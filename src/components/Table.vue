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
            <th scope="col">Description</th>
            <th scope="col">Image</th>
            <th scope="col">Edit</th>
            <th scope="col">Delete</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <th scope="row">1</th>
            <td>Estopa</td>
            <td>19 Oct 2024</td>
            <td>Yes</td>
            <td>No</td>
            <td>7,500</td>
            <td>Plaza de Toros El Bibio, Gijón</td>
            <td></td>
            <td><button><EditIcon /></button></td>
            <td><button><TrashIcon /></button></td>
          </tr>
          <tr>
            <th scope="row">2</th>
            <td>The Hardkiss</td>
            <td>26 Oct 2024</td>
            <td>Yes</td>
            <td>No</td>
            <td>1,100</td>
            <td>Patioh de la Laboral, Gijón</td>
            <td></td>
            <td><button><EditIcon /></button></td>
            <td><button><TrashIcon /></button></td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Nach</td>
            <td>31 Oct 2024</td>
            <td>Yes</td>
            <td>No</td>
            <td>500</td>
            <td>Sir Lauren's, Oviedo</td>
            <td></td>
            <td><button><EditIcon /></button></td>
            <td><button><TrashIcon /></button></td>
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
    components: {
      EditIcon,
      TrashIcon
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
    background-color: #f2f2f2;
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
    background-color: #ff728f;
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
  