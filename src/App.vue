<script>
import axios from 'axios';
import Chat from './components/Chat.vue';
export default {
  data() {
    return {
      userName1: "",
      userName2: "",
      userImg1: "",
      userImg2: "",
      users: [],

      message1: "",
      message2: "",
      messageUsers: [],

      color1: "#",
      color2: "#",
    }
  },
  components:{
    Chat
  },
  methods: {
    async getUsers() {
      try {
        const url = 'https://randomuser.me/api?results=2';
        const { data } = await axios.get(url);
        this.userName1 = `${data.results[0].name.first} ${data.results[0].name.last}`;
        this.userName2 = `${data.results[1].name.first} ${data.results[1].name.last}`;
        this.userImg1 = data.results[0].picture.large;
        this.userImg2 = data.results[1].picture.large;
      } catch (error) {
        console.log(error);
      }

    },
    sendMessageUser1() {
      this.messageUsers.push(this.userName1);
      this.messageUsers.push(this.message1);

    },
    sendMessageUser2() {
      this.messageUsers.push(this.userName2);
      this.messageUsers.push(this.message2);
    }
  },
  mounted() {
    this.getUsers();
  },
  computed: {
    fotosUsers() {
      return this.user1.map((user) => user.picture.large);
    }
  }
}
</script>

<template>
  <div class="container">
    <div id="sectionChat">
      <div class="user1">
        <img :src="userImg1" alt="">
        <p>{{ userName1 }}</p>
        <input type="color" v-model="color1">
        <textarea rows="8" v-model="message1"></textarea>
        <button @click="sendMessageUser1" >Enviar</button>
      </div>

      <Chat :users="users"  :messages="messageUsers"/>

      <div class="user2">
        <img :src="userImg2" alt="">
         <p>{{ userName2 }}</p>
        <input type="color" v-model="color2">
        <textarea rows="8" v-model="message2" ></textarea>
        <button @click="sendMessageUser2">Enviar</button>
      </div>

    </div>

  </div>
</template>

<style scoped>
.container {
  width: 100%;
  display: flex;
  justify-content: center;
}

#sectionChat {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.user1,
.user2 {
  width: 200px;
  padding: 10px;
}

p {
  margin: 4px 0px;
}

.user2 p {
  float: right;
}

img,
button {
  width: 100%;
}

input,
textarea {
  width: 100%;
  margin: 4px 0;
}

textarea {
  width: 195px;
  resize: none;
}
</style>
