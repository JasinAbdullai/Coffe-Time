<template>
  <div id="new-employee">
    <h3>Neuer Mitarbeiter</h3>
    <div class="row">
    <form @submit.prevent="saveEmployee" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="user" required>
          <label>Mitarbeiter ID#</label>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="name" required>
          <label>Name</label>
        </div>
      </div>
      <button type="submit" class="btn">Submit</button>
      <router-link to="/" class="btn grey">Cancel</router-link>
    </form>
  </div>
  </div>
</template>


   
<script>
/*  import db from './firebaseInit'
  export default {
    name: "new-employee",
    data(){
        return {
        employee_id: null,
        name: null,
        dept: null,
        position: null
      }
    },
    methods: {
      saveEmployee(){
        db.collection('employees').add({
          user: this.user,
          name: this.name,
    
        }).then(docRef => {      
          this.$router.push('/')
        }).catch(err => {
          window.log(err)
        })
      }
    }
  }  */
</script>
