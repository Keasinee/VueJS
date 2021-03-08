<template>
    <div id="employee">
        <p v-if="employees.length < 1" class="empty-table">
            No employee !!!!
        </p>
        <table class="table-style">
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Age</th>
                    <th></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="e in employees" :key="e.id">
                    <td v-if="editing === e.id">
                        <input type="text" v-model="e.name">
                    </td>
                    <td v-else>{{e.name}}</td>
                     <td v-if="editing === e.id">
                        <input type="text" v-model="e.email">
                    </td>
                    <td v-else>{{e.email}}</td>
                    <td v-if="editing === e.id">
                        <input type="text" v-model="e.age">
                    </td>
                    <td v-else>{{e.age}}</td>
                    <td style="text-align:center;" v-if="editing === e.id">
                        <button class="button-save" @click="editEmployee(e)">Save</button>
                        <button class="muted-button button-delete" @click="cancelEdit(e)">Cancel</button>
                    </td>
                    <td style="text-align:center;" v-else>
                        <button class="button-edit" @click="editMode(e)">Edit</button>
                        <button class="button-delete" @click="$emit('delete:employee',e.id)">Delete</button>
                    </td>
                </tr>
               
            </tbody>
        </table>
    </div>
</template>
<script>
export default {
    name: 'employee-table',
    data(){
        return{
            editing:null,
        }
    },
    methods:{
        editMode(employee){
            this.cachedEmployee = Object.assign({}, employee)
            this.editing = employee.id
        },
        cancelEdit(employee){
            Object.assign(employee, this.cachedEmployee)
            this.editing = null
        },
        editEmployee(employee){

            //check null
            if(employee.name === '' || employee.email === '') return

            //sending data update 
            this.$emit('edit:employee',employee.id,employee)
            this.editing = null
        }
    },
    props:{
        employees:Array
    }
}
</script>
<style scoped>
input[type=text], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
.table-style {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}
.table-style td, .table-style th {
  border: 1px solid #ddd;
  padding: 8px;
}
.table-style tr:nth-child(even){background-color: #f2f2f2;}
.table-style tr:hover {background-color: #ddd;}
.table-style th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  background-color: #150f6e;
  color: white;
}

.button-save {
  background-color: #09c231; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 10px;
}
.button-save:hover,button-save:active,button-save:focus {
    background-color:rgb(10, 146, 39);
}

.button-edit {
  background-color: #d4c70b; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 10px;
}
.button-edit:hover,button-edit:active,button-edit:focus {
    background-color:rgb(206, 168, 1);
}

.button-delete {
  background-color: #d40b0b; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 10px;
}
.button-delete:hover,button-delete:active,button-delete:focus {
    background-color:rgb(146, 12, 12);
}
.empty-table{
    font-size: 20px;
    font-weight: bold;
    background-color: #e9e4a1c2;
    color: #000;
    padding: 8px 8px;
    border-radius: 5px;
    text-align: center;
}
</style>