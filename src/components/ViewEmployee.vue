<template>
  <div id='view-employee'>
    <ul class='collection with-header'>
      <li class='collection-header'><h4>{{name}}</h4></li>
      <li class='collection-item'>Mirarbeiter ID: {{user}}</li>
    </ul>
    <router-link to="/" class="btn grey">Back</router-link>
    <button @click="deleteEmployee" class="btn red">Delete</button>

    <div class="fixed-action-btn">
      <router-link
        v-bind:to="{name: 'edit-employee', params: {user: user}}"
        class="btn-floating btn-large red">
        <i class="fa fa-pencil"></i>
      </router-link>
    </div>
  </div>
</template>

<script>
  import db from './firebaseInit'
  export default {
    name: "view-employee",
    data(){
      return {
        employee_id: null,
        name: null
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
      fetchData() {
        db.collection('user')
        .where('user','==',this.$route.params.user)
        .get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            this.user = doc.data().user
            this.name = doc.data().name

          })
        })
      },
      deleteEmployee(){
        if (confirm('Bist du sicher')) {
          db.collection('user')
            .where('user','==',this.$route.params.user)
            .get()
            .then(querySnapshot => {
              querySnapshot.forEach(doc => {
                doc.ref.delete()
                this.$router.push('/')
              })
            })
        }
      }
    }
  }
</script>
