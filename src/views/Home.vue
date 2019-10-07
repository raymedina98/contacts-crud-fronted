<template>
  <div class="container">
  <div class="row align-items-center">
    <div class="col">
    </div>
    <div class="col">
    <b-card
        border-variant="secondary"
        header="Contacts"
        header-border-variant="secondary"
        align="center"
    >
    <div class="row align-items-start">
      <div class="col">
        <router-link to="/create">
          <button class="btn btn-dark">New Contact</button>
        </router-link>
      </div>
    </div>
    <br>
    <b-list-group v-bind:key="contact.id" v-for="contact in contacts">
      <Contact v-bind:contact="contact" v-on:edit-contact="editContact" />
    </b-list-group>
    </b-card>
    </div>
    <div class="col"></div>
  </div>
    <b-modal id="modal-edit" title="Update Contact" @ok="saveUpdate"  ok-title="Save">
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

      </form>
    </b-modal>        
  </div>
</template>

<script>
// @ is an alias to /src
import Contact from '../components/Contact';
import axios from 'axios';

export default {
  name: 'home',
  components: {
    Contact
  },
  data(){
      return {
          contacts : [],
          name : '',
          phone : '',
          group : '',
          email : '',
          company : '',
          idUpdate : ''
      }
  },
  methods : {
    editContact(contact){
      this.idUpdate = contact[0];
      this.name = contact[1];
      this.phone = contact[2];
      this.group = contact[3];
      this.email = contact[4];
      this.company = contact[5];
    },
    saveUpdate(){
      axios.put(`api/contacts/${this.idUpdate}`,{
        name : this.name,
        phone : this.phone,
        group : this.group,
        email : this.email,
        company : this.company        
      })
      .then( res => console.log(res))
      .catch( err => console.log(err));
      location.reload();
    }
  },
  created(){
        axios.get('api/contacts/')
        .then( res => {
          console.log(res.data)
          this.contacts = res.data;
        })
        .catch( err => console.log(err));
  }
}
</script>
