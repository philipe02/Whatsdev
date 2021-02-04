<template>
  <div class="chat-area">
    <div class="image full-width full-height">
      <Message
        v-for="item in messages"
        :key="item.id"
        :text="item.text"
        :hour="item.hour"
        :my="my(item.userId)"
      />
    </div>
  </div>
</template>

<script>
import Message from "src/components/Message/Index";
import api from "src/services/api";
import { notify } from "src/utils";
export default {
  name: "ChatArea",
  data() {
    return {
      messages: [],
      myId: localStorage.getItem("myId"),
    };
  },
  props: ["currentUser", "newMessages"],
  components: {
    Message,
  },
  async mounted() {
    this.getMessages();
  },
  watch: {
    async currentUser() {
      this.messages = [];
      await this.getMessages();
    },
    async newMessages() {
      await this.getMessages();
    },
  },
  methods: {
    async getMessages() {
      await api
        .get(`message/${this.currentUser}/${this.myId}`)
        .then((response) => {
          this.messages = response.data;
        })
        .catch(() => {
          //notify('negative', "Falha ao listar mensagens")
        });
    },
    my(messageUserId) {
      console.log(messageUserId);
      return this.myId === messageUserId.toString();
    },
  },
};
</script>

<style lang="scss" scoped>
.chat-area {
  height: calc(100vh - 59px - 62px);
  min-width: 800px;
  width: calc(100vw - 410px);
  background-color: $grey-background;
}
.image {
  background-image: url("../../assets/background.png");
  overflow: auto;
  display: flex;
  flex-direction: column-reverse;
}
</style>