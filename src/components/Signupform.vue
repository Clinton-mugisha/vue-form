<template>
  <form @submit.prevent="formsubmit">
    <label>Email</label>
    <input type="email" required v-model="email">
     <label>Password</label>
    <input type="password" required v-model="password">
    <div v-if="passworderror" class="error">{{passworderror}}</div>
    <label >Role</label>
    <select v-model='role'>
      <option value="developer">Webdeveloper</option>
      <option value="designer">Webdesigner</option>
    </select>
    <label for="">Skills</label>
    <input type="text" v-model="tempskill" @keyup.alt="addskill">
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="remove(skill)">{{ skill }}</span>

    </div>
    <div class="submit"> 
      <button type="submit" >Submit</button></div>
    
  </form>
  <p>{{email}}</p>
    <p>{{password}}</p>
    <p>{{role}}</p>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      tempskill: '',
      skills: [],
      passworderror: ''
    }
    },
     methods: {
      addskill(e) {
        if(e.key===  ',' && this.tempskill){
          this.skills.push(this.tempskill)
          this.tempskill = ''
        }

        
      },
      remove(skill){
        this.skills = this.skills.filter((item)=>{
          return skill !== item
        })

      },
      formsubmit(){
        this.passworderror= this.password.length >5 ? '' : 'password should be more than 5'

      }
  }

}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
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
    width: 400px;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;

}
.pill{
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  font-weight: bold;
  letter-spacing: 1px;
  color: #777;
  cursor: pointer;


}
button{
  background-color:rgb(67, 67, 223);
  color: white;
  border-radius: 20px;
  border: 0;
  margin-top: 20px;
  padding: 10px 20px;
  

}
.submit{
  text-align: center;
}
.error{
  border: 0;
  border-top: 1px solid red;
  font-size: 0.8rem;
  font-weight: bold;
  color: red;
  

}
</style>