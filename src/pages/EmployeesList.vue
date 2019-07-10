<template>
    <div class="page employees-list">
        <h1 class="employees-list__header">Employees</h1>
        <div v-if="loading" class="employees-list__loading">Loading...</div>
        <table v-else>
            <thead>
                <tr >
                    <th>Id</th>
                    <th>Name</th>
                    <th>Address</th>
                    <th>Phone</th>
                    <th>Email</th>
                    <th>Edit</th>
                </tr>
            </thead>
            <tbody  v-for="employee in employees" v-bind:key="employee.id">
                <tr>
                    <td data-label="Id" v-if="selectedId !== employee.id">{{employee.id}}</td>
                    <td data-label="Id" v-if="selectedId === employee.id"><input  v-model="employee.id"/></td>

                    <td data-label="Name" v-if="selectedId !== employee.id">{{employee.name}}</td> 
                    <td data-label="Name" v-if="selectedId === employee.id"><input  v-model="employee.name"/></td>

                    <td data-label="Adress" v-if="selectedId !== employee.id">{{employee.address.street}} {{employee.address.suite}} {{employee.address.city}}</td>
                    <td data-label="Adress" v-if="selectedId === employee.id">
                        <input  v-model="employee.address.street"/> 
                        <input  v-model="employee.address.suite"/> 
                        <input  v-model="employee.address.city"/>
                    </td>

                    <td data-label="Phone" v-if="selectedId !== employee.id">{{employee.phone}}</td>
                    <td data-label="Phone" v-if="selectedId === employee.id"><input  v-model="employee.phone"/></td>
                    
                    <td data-label="Email" v-if="selectedId !== employee.id"><a :href="`mailto:${ employee.email }`">{{employee.email}}</a></td>
                    <td data-label="Email" v-if="selectedId === employee.id"><input  v-model="employee.email"/></td>

                    <td data-label="Edit">
                        <button v-if="selectedId !== employee.id" v-on:click="editModeHandler(employee.id)">Edit</button> 
                        <button v-if="selectedId === employee.id" v-on:click="editModeHandler">Back</button> 
                        <EditButton :employeeData="employee" v-if="selectedId === employee.id" @cancelEditMod="editModeHandler"/> 
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
    import axios from 'axios';
    import EditButton from '../components/EditButton';

    export default {
        components: {
            EditButton
        },
        data() {
            return {
                loading: false,
                employees: [],
                selectedId: true
            }
        },
        created () {
            this.fetchData()
        },
        watch: {
            '$route': 'fetchData'
        },
        methods: {
            fetchData () {
                this.loading = true;

                axios.get('https://jsonplaceholder.typicode.com/users')
                    .then(({data}) => {
                        this.employees = data;
                    })
                    .finally(() => {
                        this.loading = false;
                    })
            },
            editModeHandler (id){
                this.selectedId = id
            }
        }
    };

</script>
<style lang="scss" scoped>
   table {
    border: 1px solid #ccc;
    width: 100%;
    margin:0;
    padding:0;
    border-collapse: collapse;
    border-spacing: 0;
  }

  table tr {
    border: 1px solid #ddd;
    padding: 5px;
  }

  table th, table td {
    padding: 10px;
    text-align: center;
  }

  table th {
    text-transform: uppercase;
    font-size: 14px;
    letter-spacing: 1px;
  }

  @media screen and (max-width: 1024px) {

    table {
      border: 0;
    }

    table thead {
      display: none;
    }

    table tr {
      margin-bottom: 10px;
      display: block;
      border-bottom: 2px solid #ddd;
    }

    table td {
      display: block;
      text-align: right;
      font-size: 13px;
      border-bottom: 1px dotted #ccc;
    }

    table td:last-child {
      border-bottom: 0;
    }

    table td:before {
      content: attr(data-label);
      float: left;
      text-transform: uppercase;
      font-weight: bold;
    }
}
</style>