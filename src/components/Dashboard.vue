<template>
  <div id='dashboard'>
    <ul class='collection with-header'>
      <li class='collection-header'>
        <h4>Mitarbeiter</h4>
      </li>
      <li
        v-for="user in users"
        v-bind:key="user"
        class="collection-item">
        {{employee.employee_id}}:{{employee.name}}
        <router-link
          class="secondary-content"
          v-bind:to="{name: 'view-employee', params: {user}}">
        <i class="fa fa-eye"></i></router-link>
      </li>
    </ul>
    <div class="fixed-action-btn">
      <router-link
        to="/new"
        class="btn-floating btn-large red">
        <i class="fa fa-plus"></i>
      </router-link>
    </div>
  </div>
</template>

<script>
  import db from './firebaseInit'
  export default {
    name: "dashboard",
    data(){
      return {
        user: []
      }
    },
    created(){
      db.collection('user').get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            const data = {

              'user': doc.data().user,
              'name': doc.data().name, 
            }
            this.user.push(data)
          })
        })
    }
  }
</script>
