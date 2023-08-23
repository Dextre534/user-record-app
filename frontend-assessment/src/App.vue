<template class="mt-0">
  <div class="square"></div>
  <div class="container">
    <!-- Nav Bar -->
    <nav class="navbar navbar-expand-lg navbar-light ">
      <img alt="Kiratech logo" src="./assets/logo.png" class="banner-logo">
    </nav>

    <!-- User Banner -->
    <div class="row mb-5 mt-4">
    
      <div class="col-2">
        <img alt="Avatar img" src="./assets/Avatar.png" class="avatar-img float-start">
      </div>

      <div class="col-2 ms-5">
        <h2 class="text-start mt-4 text-white fw-bold">John Doe</h2>
        <p class="text-start text-white">Last online: 2 days ago</p>
      </div>

      <div class="col-4 text-start d-flex align-items-start ms-2 mt-5">
        <button class="btn button-white fw-bold ps-4 pe-4 pt-2 pb-2">Send Message</button>
        <button class="btn button-blue fw-bold ms-3 ps-4 pe-4 pt-2 pb-2">Add friend</button>
      </div>
    </div>

    <div class="mb-5 d-flex flex-row">
      <input type="text" class="form-control" v-model="searchKeyword"> 
      <button class="btn button-blue ms-3" @click="searchUser">Search</button>
      <button class="btn button-white ms-3" @click="resetSearch">Reset</button>
    </div>

    <!-- User records -->
    <!-- Table Headings-->
    <div class="row p-4 ">
      <div class="col-2 text-start fw-bold text-gray">
        Date of Birth
      </div>

      <div class="col-3 text-start fw-bold text-gray">
        Name
      </div>

      <div class="col-2 text-start fw-bold text-gray">
        Gender
      </div>

      <div class="col-2 text-start fw-bold text-gray">
        Country
      </div>

      <div class="col-3 text-end fw-bold text-gray">
        Email
      </div>
    </div>

    <!-- If there are no search results, show list of all users -->
    <div v-if="!searchResults.length">
      <user-record
        v-for="(user, index) in users"
        :key="user.id.name"
        :index="index"
        :date="dateConvert(user.dob.date)"
        :name="user.name.first + ' ' + user.name.last"
        :gender="user.gender"
        :country="user.location.country"
        :email="user.email"
        @click="showModal(index, 'users')"
      ></user-record>
    </div>

    <!-- else show list of users in search results array -->
    <div v-else>
      <user-record
        v-for="(user, index) in searchResults"
        :key="user.id.name"
        :index="index"
        :date="dateConvert(user.dob.date)"
        :name="user.name.first  + ' ' + user.name.last"
        :gender="user.gender"
        :country="user.location.country"
        :email="user.email"
        @click="showModal(index, 'search')"
      ></user-record>
    </div>

    <!-- Modal popup component -->
    <user-modal
      :user="userSelected"
      :show="isModalVisible"
      @close="closeModal"
    ></user-modal>

    <button class="btn button-blue mb-5 mt-4 ps-5 pe-5" @click="loadUsers"> Refresh </button>

  </div>
  
</template>


<script>
import UserRecord from './components/UserRecord.vue'
import UserModal from './components/UserModal.vue'

export default {
  name: 'App',
  components: {
    UserRecord,
    UserModal
  },
  data() {
    return {
      users: [], // Array to store user objects
      userSelected: null,
      searchKeyword: '',
      searchResults: [], // Array to store user objects from search
      isModalVisible: false,
    };
  },
  methods: {
    dateConvert(datestr) { // Method to convert date to different format
      let date1 = new Date(datestr)
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      const formattedDate = date1.toLocaleDateString(undefined, options);
      return(formattedDate)
    },
    loadUsers() {
      this.searchKeyword = '';
      this.searchResults = []
      fetch('https://randomuser.me/api/?results=20')
        .then((response) => {
            if (response.ok) {
              return response.json();
            }
          }
        ).then((data) =>{
          this.users = data.results;
        })
    },
    showModal(index, term) { // term parameter is used to determine which array to get user data from
      this.isModalVisible = true;
      if (term === 'users'){
        this.userSelected = this.users[index];
      } else if (term === 'search') {
        this.userSelected = this.searchResults[index];
      }
      
    },
    closeModal() {
      this.isModalVisible = false;
    },
    searchUser() {
      this.searchResults = []
      let keyword = this.searchKeyword.toLowerCase();

      for (const item of this.users) {
        for (const key in item) { // For each object in user match the keyword
          if (typeof item[key] === 'string' && item[key].toLowerCase() === keyword) {
            this.searchResults.push(item);
          }
          if (typeof item[key] === 'object') { // If the object is not a String, iterate through the keys in it
            for (const nestedKey in item[key]) {
              if (typeof item[key][nestedKey] === 'string' && item[key][nestedKey].toLowerCase() === keyword) {
                this.searchResults.push(item);
              }
            }
          }
        }
      }
    },
    resetSearch() {
      this.searchKeyword = '';
      this.searchResults = [];
    }
    
  },
  mounted() { // Load users list on mount
    this.loadUsers();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.banner-logo {
  height: 60px;
}

.square {
  background-color:#46b4c7;
  top:8%;
  height:15%;
  width:100%;
  position: absolute;
  z-index: -1;
}

.avatar-img {
  height: 180px;
}

.inline-b{
  display: inline-block;
}

.button-white{
  background-color: white !important;
  color:#46b4c7 !important;
  border: 1px solid #46b4c7 !important;
}

.button-white:hover {
  background-color: #46b4c7 !important;
  color:white !important;
  border-color: white !important;
}

.button-blue{
  background-color: #46b4c7 !important;
  color:white !important;
  border-color: white !important;
}

.button-blue:hover{
  background-color: white !important;
  color:#46b4c7 !important;
  border: 1px solid #46b4c7 !important;
}

.text-gray{
  color:lightgray
}

.user-rec:hover{
  border: 10px;
  border-color: #46b4c7 ;
}

@media only screen and (max-width: 1900px) {
  .square {
    background-color:#46b4c7;
    top: 12%;
    height: 20%;
    width:100%;
    position: absolute;
    z-index: -1;
  }

}
</style>
