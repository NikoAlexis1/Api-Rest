<template>
    <div class="chat">
        <div v-if="messages.length > 0">
            <p v-for="message in messages">{{ message }}</p>
        </div>
    </div>

</template>

<script>
export default{
    props:{
        users: Object,
        messages: Object,
    },
    computed: {
    lastMessage() {
      return this.messages[this.messages.length - 1];
    }
  }
}
</script>
<style scoped>
.chat {
  width: 100%;
  background-color: antiquewhite;
  box-shadow: 0px 0px 3px 3px #888888;
}
</style>