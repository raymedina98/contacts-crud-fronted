<template>
   <div class="container">
  <div class="row align-items-center">
    <div class="col"></div>
    <div class="col">
    <b-card
        border-variant="secondary"
        header="Create a new contact"
        header-border-variant="secondary"
        align="center"
    >
    
      <form>
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" v-model="name" class="form-control" id="name"  placeholder="Enter the contact name">
          </div>
          <div class="form-group">
            <label for="phone">Phone</label>
            <input type="number" v-model="phone" class="form-control" id="phone" placeholder="Enter the contact phone with the area code" >
          </div>
          <div class="form-group">
            <label for="group">Group</label>
            <input type="text" v-model="group" class="form-control" id="group" placeholder="Enter the contact group" >
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" v-model="email" class="form-control" id="email" placeholder="Enter the contact email" >
          </div> 
          <div class="form-group">
            <label for="company">Company</label>
            <input type="text" v-model="company" class="form-control" id="company" placeholder="Enter the company name" >
          </div>
            <button type="submit" v-on:click.prevent="createContact" class="btn btn-dark">Create</button>
            <router-link to="/">
              <button class="btn btn-info">Cancel</button>
            </router-link>
      </form>
    </b-card>
    </div>
    <div class="col"></div>
  </div>
  
  </div>
</template>

<script>

import axios from 'axios';
import router from '../router'

export default{

  name : 'create',
  data(){
    return {
      name : '',
      phone : '',
      group : '',
      email : '',
      company : ''
    }
  },
  methods : {
    createContact(){
      axios.post('api/contacts/', {
        name : this.name,
        phone : this.phone,
        group : this.group,
        email : this.email,
        company : this.company
      })
        .then( res => {
          console.log(res.data);
          router.push({path: '/'});
        })
        .catch( err => console.log(err));
    }
  }
}
</script>
