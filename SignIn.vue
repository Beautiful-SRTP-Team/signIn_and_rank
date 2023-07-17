<template>
  <v-container class="fill-height">

    <v-dialog
      v-model="open"
      fullscreen
      :scrim="false"
      transition="dialog-bottom-transition"
    >
      <template v-slot:activator="{ props }">
        <v-btn
          color="primary"
          dark
          v-bind="props"
        >
          签到打卡
        </v-btn>
      </template>
      <v-card>
        <v-toolbar
          dark
          color="Coral"
        >
          <v-btn
            icon
            dark
            @click="clickMe"
          >
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>签到打卡</v-toolbar-title>
        </v-toolbar>


        <!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片-->
        <!--顶端卡片-->
        <v-card
          class="mx-auto"
          width="100%"
          height="50%"
        >
          <v-img
            src="../assets/20200312173221_nufod.jpg"
            height="80%"
            cover
          ></v-img>

          <v-card-title>
            坚持打卡的小朋友最棒
          </v-card-title>

          <v-card-subtitle>
            一点一点在进步
          </v-card-subtitle>

          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn
              :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
              @click="show = !show"
            ></v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="show">
              <v-divider></v-divider>

              <v-card-text>
                加油
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
        <!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片--><!--顶端卡片-->
        <!--顶端卡片-->


        <v-list
          lines="two"
          subheader
        >
          <v-list-subheader>User Controls</v-list-subheader>
          <v-list-item title="Content filtering"
                       subtitle="Set the content filtering level to restrict apps that can be downloaded"></v-list-item>
          <v-list-item title="Password"
                       subtitle="Require password for purchase or use password to restrict purchase"></v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list :items="tops"
                item-value="order"
                item-title="msg"
        ></v-list>
        <!--以上的list就是我们的排行榜数据-->
        <v-divider></v-divider>
        <v-container>
          <v-btn
            icon
            dark
            @click="postData"
          >签到
          </v-btn>
        </v-container>

      </v-card>
    </v-dialog>
  </v-container>
</template>

<script setup>

import {createApp, ref} from "vue";
import axios from 'axios';
import SignIn from "@/components/SignIn.vue";

const SI = createApp(SignIn)
SI.config.globalProperties.$axios = axios;
const url = "";  //================================URL在这里=================================//
const tops = [
  {
    order: 1,
    name: "A", score: 11
  },
  {
    order: 2,
    name: "B", score: 1
  },
].map((v) => {
  return {msg: `姓名：${v.name} 分数：${v.score}`, order: v.order}
})

const open = ref(false)
const clickMe = () => {
  open.value = !open.value
}

const postData = () => {
  const data = {username: 'clever_ik', signInFlag: 1};
  fetch(url, {
    method: 'POST', // or 'PUT'
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(data),
  })
    .then(response => response.json())
    .then(data => {
      console.log('Success:', data);
    })
    .catch((error) => {
      console.error('Error:', error);
    });

}
const show = ref(false)
</script>


<style scoped>

</style>
