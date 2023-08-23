<template>
    <Transition name="modal">
      <div v-if="show" class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-container">
            
            <div class="row">
                <div class="col-10">
                    <h1 class="text-start fw-bold mb-3">{{ user.name.first }} {{ user.name.last }}</h1>
                </div>
                <div class="col">
                    <button class="btn-close" @click="$emit('close')"></button>
                </div>
                
            </div>

            <div class="row text-start mb-2">
                <div class="col-3">
                    Date:
                </div>
                <div class="col">
                    {{ dateConvert(user.dob.date) }}
                </div>
            </div>

            <div class="row text-start mb-2">
                <div class="col-3">
                    Phone:
                </div>
                <div class="col">
                    {{ user.phone }}
                </div>
            </div>

            <div class="row text-start mb-2">
                <div class="col-3">
                    Gender:
                </div>
                <div class="col">
                    {{ user.gender }}
                </div>
            </div>

            <div class="row text-start mb-2">
                <div class="col-3">
                    Country:
                </div>
                <div class="col">
                    {{ user.location.country }}
                </div>
            </div>

            <div class="row text-start mb-2">
                <div class="col-3">
                    Email:
                </div>
                <div class="col">
                    {{ user.email }}
                </div>
            </div>
            
          </div>
        </div>
      </div>
    </Transition>
  </template>
  
  
  <script>
  
  export default {
    name: 'UserModal',
    props: [
        'show',
        'user',
    ],
    methods:{
        dateConvert(datestr) {
            let date1 = new Date(datestr)
            const options = { year: 'numeric', month: 'long', day: 'numeric' };
            const formattedDate = date1.toLocaleDateString(undefined, options);
            return(formattedDate)
        },
    }
  }
  </script>

  <!-- 
    Modal code taken and modified from
    https://popupsmart.com/blog/vue-modal-and-popup#:~:text=Also%2C%20you%20can%20use%20vue,need%20triggers%20to%20be%20activated.
  -->
  
  <style>
  .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: table;
    transition: opacity 0.3s ease;
  }
  
  .modal-wrapper {
    display: table-cell;
    vertical-align: middle;
  }
  
  .modal-container {
    width: 45%;
    height: 40%;
    margin: 0px auto;
    padding: 20px 30px;
    background-color: #fff;
    border-radius: 15px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
  }
  
  /* .modal-body {
    margin: 20px 0;
  } */
  
  .modal-default-button {
    float: right;
  }
  
  /*
   * The following styles are auto-applied to elements with
   * transition="modal" when their visibility is toggled
   * by Vue.js.
   *
   * You can easily play with the modal transition by editing
   * these styles.
   */
  
  .modal-enter-from {
    opacity: 0;
  }
  
  .modal-leave-to {
    opacity: 0;
  }
  
  .modal-enter-from .modal-container,
  .modal-leave-to .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
  </style>
  