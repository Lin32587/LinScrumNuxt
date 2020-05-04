<template>
  <v-dialog v-model="dialog" persistent max-width="400px">
    <template v-slot:activator="{ on }">
      <v-btn color="primary" dark v-on="on">登录</v-btn>
    </template>
    <v-card>
      <v-img
        class="white--text align-end"
        height="200px"
        src="https://images.unsplash.com/photo-1550645612-83f5d594b671?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80"
      >
        <v-card-title>Login and Let's do it</v-card-title>
      </v-img>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field label="用户名或邮箱" required ></v-text-field>
              <!-- <small class="red--text">未找到已注册邮箱</small> -->
            </v-col>
            <v-col cols="12">
              <v-text-field label="用户密码" type="password" required ></v-text-field>
              <!-- <small class="red--text">密码错误</small> -->
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" @click="dialog = false">确定</v-btn>
        <v-btn color="blue darken-1" text @click="dialog = false">取消</v-btn>
        <v-spacer></v-spacer>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    dialog: false
  })
};
</script>

<style>
</style>
