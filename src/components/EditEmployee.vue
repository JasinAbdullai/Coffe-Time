<template>
  <div id="new-employee">
    <h3>Mitarbeiter bearbeiten </h3>
    <div class="row">
    <form @submit.prevent="updateEmployee" class="col s12">
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="employee_id" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="name" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="dept" required>
        </div>
      </div>
      <div class="row">
        <div class="input-field col s12">
          <input type="text" v-model="position" required>
        </div>
      </div>
      <button type="submit" class="btn">Submit</button>
      <router-link to="/" class="btn grey">Cancel</router-link>
    </form>
  </div>
  </div>
</template>

<script>
  import db from './firebaseInit'
  export default {
    name: "edit-employee",
    data(){
      return {
        employee_id: null,
        name: null,
      }
    },
    beforeRouteEnter(to, from, next){
      db.collection('user')
        .where('user','==',to.params.user)
        .get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            next(vm => {
              vm.employee_id = doc.data().employee_id
              vm.name = doc.data().name
            })
          })
        })
    },
    watch: {
      '$route': 'fetchData'
    },
    methods: {
      fetchData(){
        db.collection('user')
          .where('user','==',this.$route.params.user)
          .get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              this.employee_id = doc.data().employee_id
              this.name = doc.data().name
            })
          })
      },
      updateEmployee(){
        db.collection('user')
          .where('user','==',this.$route.params.user)
          .get()
          .then(querySnapshot => {
            querySnapshot.forEach(doc => {
              doc.ref.update({
                user: this.user,
                name: this.name
              }).then(()=>{
                this.$router.push({name:'view-employee', params:{employee_id: this.user}})
              })
            })
          })
      }
    }
  }
</script>
