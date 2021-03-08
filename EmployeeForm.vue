<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label>Name</label>
             <!-- ref first - ทำให้ focus ที่ field นั้นเป็น field แรก -->
            <input 
                ref="first"
                type="text" 
                :class="{'has-error' : submitting && invalidName}"
                v-model="employee.name" 
                @focus="clearStatus"
                @keypress="clearStatus"
            />

            <label>E-mail</label>
            <input 
                type="text"
                :class="{'has-error' : submitting && invalidEmail}"
                v-model="employee.email"
                @focus="clearStatus"
            />

            <label>Age</label>
            <input v-model="employee.age" type="text" />
            <br />

            <p v-if="error && submitting" class="error-message">
                Please fill out all required fields.
            </p>

            <p v-if="success" class="success-message">
               Employee Successfully added !!!
            </p>

            <button class="button">Add Employee</button>

        </form>
    </div>
</template>
<script>
export default {
    name: 'employee-form',
    data(){
        return {
            //check form
            submitting : false,

            //check error form
            error : false,

            //check data senting correct
            success:false,

            employee:{
                name: '',
                email:'',
                age:''
            }
        }
    },
    methods:{
        handleSubmit(){
            this.submitting = true
            this.clearStatus()

            //ถ้ามีการป้อน name และ email ไม่ถูกต้อง จะ return error
            if(this.invalidName || this.invalidEmail){
                this.error = true
                return
            }
            // console.log("testing handle submit !!");

            //เพิ่มข้อมูลลงไปในตาราง
            this.$emit('add:employee',this.employee);
            //focus ที่ฟิลด์แรก
            this.$refs.first.focus();

            // เซตค่าว่าง
            this.employee = {
                name: '',
                email: '',
                age: ''
            }
            //set status
            this.error = false
            this.success = true
            this.submitting = false

           
        },
        //function clear
         clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed:{

        //data incorrect

        invalidName(){
            return this.employee.name === ''
        },
        invalidEmail(){
            return this.employee.email === ''
        }
    }
}
</script>
<style scoped>
form{
    margin-bottom:2rem;
}
input[type=text], select {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

input[type=submit] {
  width: 100%;
  background-color: #4CAF50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

input[type=submit]:hover {
  background-color: #45a049;
}

div {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

.button {
  background-color: #110c58; /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 10px;
}
.button:hover,button:active,button:focus {
    background-color:rgb(43, 45, 121);
}
[class*='-message']{
    font-weight: bold;
}
.error-message{
    color:#d33c40;
}
.success-message{
    color: #45a049;
}
</style>