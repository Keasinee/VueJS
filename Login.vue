<template>
    <div class="container">
        <div class="content" id="login-form">    
            <div class="header">
                <label>Login</label>
            </div>
            <br />

            <label>E-mail</label>
            <input type="text"  v-model="data.email" placeholder="E-mail"/>

            <label>Password</label>
            <input type="password" v-model="data.password" placeholder="Password"/>

            <div class="button-footer">
                <button class="button" @click="login" >Login</button>
                <button class="button">Cancel</button>
            </div>
            
        </div>
    </div>
</template>
<script>
export default {
    name: 'login-form',

    data(){
        return{
            data : {
                email: '',
                password : ''
            },
            isLogging : true,
        }
    },
    methods:{
        login(){
           this.isLogging = false
        }
    }
}
</script>
<style scoped>
.container{
    padding: 100px;
}
.content {
    max-width: 800px;
    border-radius: 5px;
    background-color: #f2f2f2;
    padding: 20px;
    margin-left: 190px;
}
form{
    margin-bottom:2rem;
}
.header{
    font-size: 3rem;
    font-weight: 600;
    text-align: center;
    margin-bottom: 10px;
}
input[type=text], input[type=password], select {
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
.button-footer{
    text-align: center;
}
</style>