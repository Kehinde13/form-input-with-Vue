<template>
    <form @submit.prevent="handleSubmit">
     <label>Email</label>
     <input type="email" required v-model="email">

     <label>Password</label>
     <input type="password" required v-model="password">
     <p v-if="validatePassword" class="error">{{ validatePassword }}</p>

     <label>Role</label>
     <select v-model="role">
      <option value="designer" > Web Designer</option>
      <option value="developer">Web Developer</option>
     </select>

     <div>
     <input type="checkbox" v-model="terms" required>
     <label>Terms and Agreemants</label>
     </div>

     <label>Skills</label>
     <input type="text" v-model="tempSkill" @keyup="addSkill">

     <div>
       <p class="skills" v-for="skill in skills" :key="skill" >
          <span @click="deleteSkill(skill)">{{ skill }}</span>
      </p>
     </div>
    
     <div class="submit">
        <button>Create an account</button>
     </div>
     
    </form>

    <p> your email: {{ email }} </p>
    <p>your password: {{ password }}</p> 
    <p>Role: {{ role }}</p> 
    <p>Accept terms: {{ terms }}</p>
 </template>
 
 <script>
   export default {
     data(){
      return {
        email: '',
        password: '',
        role: '',
        terms: false,
        tempSkill: '',
        skills: [],
        validatePassword: ''
      }
     },
     methods: {
      addSkill(e){
       if(e.key === 'Shift' && this.tempSkill){
        if(!this.skills.includes(this.tempSkill)){
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
       }
      },
      deleteSkill(skill){
       this.skills = this.skills.filter((item) => {
         return skill !== item
       })
      },
      handleSubmit(){
       this.validatePassword = this.password.length > 5 
       ? " " : "Your Password Must be longer than 5" 

       
      }
     }
   }
 </script>
 
 <style>
   form {
     max-width: 420px;
     margin: 50px auto;
     background: white;
     text-align: left;
     padding: 40px;
     border-radius: 10px;
     border: 1px solid #555;
   }
   label {
     color: #aaa;
     display: inline-block;
     margin: 25px 0 15px;
     font-size: 0.6rem;
     text-transform: uppercase;
     letter-spacing: 1px;
     font-weight: bold;
   }
   input, select{
     display: block;
     padding: 10px 6px;
     width: 100%;
     box-sizing: border-box;
     border: none;
     border-bottom: 1px solid #ddd;
     color: #555;
   }
   input[type="checkbox"]{
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
   }
   .skills {
    display: inline-block;
    margin: 10px 2px;
    width: 20px 10px 0 0;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
   }
   button {
    background: blue;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
   }
   .submit {
    text-align: center;
   }
   .error {
    color: red;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
   }

 </style>