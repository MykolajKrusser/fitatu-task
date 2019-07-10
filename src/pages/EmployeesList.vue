<template>
    <div class="page employees-list">
        <h1 class="employees-list__header">Employees</h1>
        <div v-if="loading" class="employees-list__loading">Loading...</div>
        <table v-else class="employees-list__list">
            <tr class="employees-list__list-header">
                <th>id</th>
                <th>Name</th>
                <th>Address</th>
                <th>Phone</th>
                <th>Email</th>
                <th>Edit</th>
            </tr>
            <tr v-for="employee in employees" v-bind:key="employee.id" class="employees-list__list-row">
                <td v-if="selectedId !== employee.id">{{employee.id}}</td>
                <td v-if="selectedId === employee.id"><input  v-model="employee.id"/></td>

                <td v-if="selectedId !== employee.id">{{employee.name}}</td> 
                <td v-if="selectedId === employee.id"><input  v-model="employee.name"/></td>

                <td v-if="selectedId !== employee.id">{{employee.address.street}} {{employee.address.suite}} {{employee.address.city}}</td>
                <td v-if="selectedId === employee.id">
                    <input  v-model="employee.address.street"/> 
                    <input  v-model="employee.address.suite"/> 
                    <input  v-model="employee.address.city"/>
                </td>

                <td v-if="selectedId !== employee.id">{{employee.phone}}</td>
                <td v-if="selectedId === employee.id"><input  v-model="employee.phone"/></td>
                
                <td v-if="selectedId !== employee.id"><a :href="`mailto:${ employee.email }`">{{employee.email}}</a></td>
                <td v-if="selectedId === employee.id"><input  v-model="employee.email"/></td>

                <td>
                    <button v-if="selectedId !== employee.id" v-on:click="editModeHandler(employee.id)">Edit</button> 
                    <button v-if="selectedId === employee.id" v-on:click="editModeHandler">Back</button> 
                    <EditButton :employeeData="employee" v-if="selectedId === employee.id" @cancelEditMod="editModeHandler"/> 
                </td>
            </tr>
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
                editMode: false,
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
    .employees-list {
        &__header {
            font-size: 20px;
            padding: 0 0 10px;
        }

        &__loading {
            color: #999d9d;
            text-align: center;
        }

        &__list {
            font-size: 14px;
            width: 100%;
            border-collapse: collapse;
        }

        &__list-header {
            background: #f7f8f9;
            border-bottom: 1px solid #999d9d;

            th {
                padding: 8px;
            }
        }

        &__list-row {
            background: #fff;

            td {
                padding: 8px;
            }
        }
    }
</style>