<template>
    <div class="page employees-list">
        <h1 class="employees-list__header">Employees</h1>
        <div v-if="loading" class="employees-list__loading">Loading...</div>
        <table v-else class="employees-list__list">
            <thead>
                <tr class="employees-list__list-header">
                    <th>Id</th>
                    <th>Name</th>
                    <th>Address</th>
                    <th>Phone</th>
                    <th>Email</th>
                    <th>Edit</th>
                </tr>
            </thead>
            <tbody  v-for="employee in employees" v-bind:key="employee.id">
                <tr v-if="selectedId !== employee.id" class="employees-list__list-row">
                    <td data-label="Id">{{employee.id}}</td>
                    <td data-label="Name">{{employee.name}}</td>
                    <td data-label="Adress">{{employee.address.street}} {{employee.address.suite}} {{employee.address.city}}</td>
                    <td data-label="Phone">{{employee.phone}}</td>
                    <td data-label="Email"><a :href="`mailto:${ employee.email }`">{{employee.email}}</a></td>
                    <td data-label="Edit">
                        <button v-if="selectedId !== employee.id" v-on:click="editModeHandler(employee.id)">Edit</button> 
                        <button v-if="selectedId === employee.id" v-on:click="editModeHandler">Back</button> 
                        <EditButton :employeeData="employee" v-if="selectedId === employee.id" @cancelEditMod="editModeHandler"/> 
                    </td>
                </tr>
                <tr v-if="selectedId === employee.id" class="employees-list__list-row">
                    <td data-label="Id"><input  v-model="employee.id"/></td> 
                    <td data-label="Name"><input  v-model="employee.name"/></td>
                    <td data-label="Adress">
                        <input  v-model="employee.address.street"/> 
                        <input  v-model="employee.address.suite"/> 
                        <input  v-model="employee.address.city"/>
                    </td>
                    <td data-label="Phone"><input  v-model="employee.phone"/></td>
                    <td data-label="Email"><input  v-model="employee.email"/></td>
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
    .employees-list{
        &__header {
            font-size: 20px;
            padding: 0 0 10px;
        }
        &__loading {
            color: #999d9d;
            text-align: center;
        }
        &__list {
            border: 1px solid #ccc;
            width: 100%;
            margin:0;
            padding:0;
            border-collapse: collapse;
            border-spacing: 0;
            text-align: left;
        }
        &__list-header{
            text-transform: uppercase;
            font-size: 14px;
            letter-spacing: 1px;
            padding: 10px;
                th{
                    padding: 10px;
                }
        }
        &__list-row{
            border: 1px solid #ddd;
            padding: 5px;
            text-align: left;
        }
        td {
            padding: 10px;
            text-align: center;
            text-align: left;
        }
    }

  @media screen and (max-width: 1024px) {
    .employees-list {
      border: 0;
      text-align: left;
        &__list{
            thead{
                display: none;
            }
        }
        &__list-row{
            margin-bottom: 10px;
            display: block;
            border-bottom: 2px solid #ddd;
        }
        td {
            display: block;
            text-align: right;
            font-size: 13px;
            border-bottom: 1px dotted #ccc;
            &:last-child{
                border-bottom: 0;
            }
            &:before{
                content: attr(data-label);
                float: left;
                text-transform: uppercase;
                font-weight: bold;
            }
        }
    }
}
</style>