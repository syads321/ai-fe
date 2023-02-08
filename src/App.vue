<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png" transition="scale-transition" width="40" />

        <v-img alt="Vuetify Name" class="shrink mt-1 hidden-sm-and-down" contain min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png" width="100" />
      </div>

      <v-spacer></v-spacer>

      <v-btn @click="testConnect()" text>
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <div id="app">
        <v-app id="inspire">
          <v-container style="max-width:400px">
            <v-row justify="space-around d-flex flex-column">
              <v-card v-for="message in messages" :key="message.time" flat>
                <v-list-item :key="message.time" v-if="message.from != 'You'" class="">
                  <v-list-item-avatar class="align-self-start mr-2">
                    <v-avatar size="40">
                      <v-img src="https://via.placeholder.com/50"></v-img>
                    </v-avatar>
                  </v-list-item-avatar>
                  <v-list-item-content class="received-message">
                    <v-card color="success" class="flex-none">
                      <v-card-text class="white--text pa-2 d-flex flex-column">
                        <span class="text-caption">{{ message.from }} </span>
                        <span class="align-self-start text-subtitle-1">{{ message.message }}</span>
                        <span class="text-caption font-italic align-self-end">{{
                          message.time
                        }}</span>
                      </v-card-text>
                    </v-card>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item v-else :key="message.time">
                  <v-list-item-content class="sent-message justify-end">
                    <v-card color="primary" class="flex-none">
                      <v-card-text class="white--text pa-2 d-flex flex-column">
                        <span class="text-subtitle-1 chat-message">{{ message.message }}</span>
                        <span class="text-caption font-italic align-self-start">{{
                          message.time
                        }}</span>
                      </v-card-text>
                    </v-card>
                  </v-list-item-content>
                  <v-list-item-avatar class="align-self-start ml-2">
                    <v-img src="https://via.placeholder.com/50"></v-img>
                  </v-list-item-avatar>
                </v-list-item>
              </v-card>
            </v-row>
          </v-container>
          <v-footer fixed>
            <v-container class="ma-0 pa-0 ml-auto mr-auto" style="max-width:400px">
              <v-row>
                <v-col>
                  <div class="d-flex flex-row align-center">
                    <v-text-field v-model="msg" placeholder="Type Something" @keypress.enter="send"></v-text-field>
                    <v-btn icon class="ml-4" @click="send"><v-icon>mdi-send</v-icon></v-btn>
                  </div>
                </v-col>
              </v-row>
            </v-container>
          </v-footer>
        </v-app>
      </div>
    </v-main>
  </v-app>
</template>

<script>

import { io } from "socket.io-client";

export default {
  name: 'App',
  data: () => ({
    messages: [
      {
        from: 'You',
        message: `Sure, I'll see you later.`,
        time: '10:42am',
        color: 'deep-purple lighten-1',
      },
      {
        from: 'John Doe',
        message: 'Yeah, sure. Does 1:00pm work?',
        time: '10:37am',
        color: 'green',
      },
      {
        from: 'You',
        message: 'Did you still want to grab lunch today?',
        time: '9:47am',
        color: 'deep-purple lighten-1',
      },
      {
        from: 'You',
        message: `Sure, I'll see you later.`,
        time: '10:42am',
        color: 'deep-purple lighten-1',
      },
      {
        from: 'John Doe',
        message: 'Yeah, sure. Does 1:00pm work?',
        time: '10:37am',
        color: 'green',
      },
      {
        from: 'You',
        message: 'Did you still want to grab lunch today?',
        time: '9:47am',
        color: 'deep-purple lighten-1',
      },
      {
        from: 'You',
        message: `Sure, I'll see you later.`,
        time: '10:42am',
        color: 'deep-purple lighten-1',
      },
      {
        from: 'John Doe',
        message: 'Yeah, sure. Does 1:00pm work?',
        time: '10:37am',
        color: 'green',
      },
      {
        from: 'You',
        message: 'Did you still want to grab lunch today?',
        time: '9:47am',
        color: 'deep-purple lighten-1',
      },
    ],
    chat: [
    ],
    msg: null,
  }),
  methods: {
    testConnect() {
      // eslint-disable-next-line 
      const socket = io('http://localhost:3000');
      console.log(socket)
    },
    send() {
      this.chat.push(
        {
          from: "user",
          msg: this.msg
        })
      this.msg = null
      this.addReply()
    },
    addReply() {
      this.chat.push({
        from: "sushant",
        msg: "Hmm"
      })
    }
  }
};
</script>
