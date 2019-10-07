<template>
<div>
        <b-list-group-item>
        <div class="row align-items-center">
          <div class="col">
            <span><img src="../assets/png/person-4x.png" alt="contact-icon"></span>
          </div>
        </div>
        <div class="row align-items-center">
          <div class="col">
            {{contact.name}}
          </div>
        </div>
        <div class="row align-items-center">
          <div class="col">
            +{{contact.phone}}
          </div>
        </div>
        <div class="row align-items-center">
          <div class="col">
            <div>
              <span v-b-modal.modal-edit v-on:click="$emit('edit-contact', [contact._id, contact.name, contact.phone, contact.group, contact.email, contact.company ])">
                  <img style="cursor:pointer;" src="../assets/png/pencil-3x.png" alt="contact-icon">
                  </span>
             </div>                   
          </div>
          <div class="col">
            <div>
              <span v-on:click="deleteContact(contact._id)"><img style="cursor:pointer;" src="../assets/png/trash-3x.png" alt="contact-icon"></span>
             
             </div>  
          </div>
          
        </div>
        
      </b-list-group-item>
            
</div>
</template>

<script>
    
import axios from 'axios';

export default {

    name : "contact",
    props : ["contact"],
    methods: {
        deleteContact(id){
            if(confirm("Are you sure to delete this contact?")){
                axios.delete(`api/contacts/${id}`)
                .then(res => console.log(res))
                .catch(err => console.log(err));
                location.reload();
            }
        }
    }
}
</script>

<style>

</style>