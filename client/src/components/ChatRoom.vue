<template>
<div>
    <button class="open-button" v-on:click.prevent='openForm'>Chat</button>
    <div class="chat-popup" id="myForm">
      <form class="form-container">
        <h1>Chat</h1>
          <div id="chatbox">
            <div v-for="chat in chats" v-bind:key="chat.id">
              <p class="text text-end" v-if='email === chat.email'>{{ chat.email }}: {{ chat.message }}</p>
              <p class="text text-start" v-else>{{ chat.email }}: {{ chat.message }}</p>
            </div>
          </div>
        <form class="mb-2" name="message" action="">
          <div class="flex justify-content-center">
            <input name="usermsg" type="text" placeholder="message" id="usermsg" v-model="chatData.chatMessage"/>
            <button class="sendbtn" id="btn-chat" v-on:click.prevent='sendMessage'>Send</button>
          </div>
        </form>

        <button class="btn cancel" v-on:click.prevent='closeForm' >Close</button>
      </form>
    </div>
</div>
</template>

<script>

export default {
  el: '#chatbox',
  name: 'ChatRoom',
  data () {
    return {
      chatData: {
        access_token: localStorage.getItem('access_token'),
        chatMessage: ''
      }
    }
  },
  methods: {
    scrollToElement () {
      const el = this.$el.getElementsByClassName('text')[this.$el.getElementsByClassName('text').length - 1]
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },
    sendMessage () {
      this.$store.dispatch('sendMessage', this.chatData)
      this.chatData.chatMessage = ''
    },
    openForm () {
      document.getElementById('myForm').style.display = 'block'
    },
    closeForm () {
      document.getElementById('myForm').style.display = 'none'
    }
  },
  watch: {
    chats (newChats, oldChats) {
      // wait to render element in html
      setTimeout(() => { this.scrollToElement() }, 100)
    }
  },
  computed: {
    chats () {
      return this.$store.state.chats
    }
  }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
  }form {
    gap: 10px;
    justify-content: center;
  }form label {
    font-size: 1.5rem;
    font-weight: bold;
  }
  #chatbox {
    text-align: left;
    margin: 0 auto;
    margin-bottom: 25px;
    padding: 10px;
    background: #fff;
    height: 400px;
    width: 95%;
    border: 1px solid #a7a7a7;
    overflow: auto;
    border-radius: 4px;
    border-bottom: 4px solid #a7a7a7;
  }
  #usermsg {
    flex: 1;
    border-radius: 4px;
    border: 1px solid #ff9800;
  }

/* chat component */
.open-button {
  background-color: #555;
  color: white;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  opacity: 0.8;
  position: fixed;
  bottom: 23px;
  right: 28px;
  width: 280px;
  z-index: 2;
}

/* The popup chat - hidden by default */
.chat-popup {
  display: none;
  position: fixed;
  bottom: 0;
  right: 15px;
  border: 3px solid #f1f1f1;
  z-index: 9;
}

/* Add styles to the form container */
.form-container {
  max-width: 300px;
  padding: 10px;
  background-color: white;
}

/* Full-width textarea */
.form-container textarea {
  width: 100%;
  padding: 15px;
  margin: 5px 0 22px 0;
  border: none;
  background: #f1f1f1;
  resize: none;
  min-height: 200px;
}

.form-container .btn {
  background-color: #04AA6D;
  color: white;
  padding: 16px 20px;
  border: none;
  cursor: pointer;
  width: 100%;
  margin-bottom:10px;
  opacity: 0.8;
}

.form-container .cancel {
  background-color: red;
  width: 280px;
}

.form-container .btn:hover, .open-button:hover {
  opacity: 1;
}

.sendbtn {
  background: greenyellow;
}

</style>
