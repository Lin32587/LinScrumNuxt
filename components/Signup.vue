<template>
  <v-dialog v-model="dialog" persistent max-width="400px">
    <template v-slot:activator="{ on }">
      <v-btn color="teal" dark v-on="on" text>注册</v-btn>
    </template>
    <v-card>
      <v-img
        class="white--text align-end"
        height="200px"
        src="https://images.unsplash.com/photo-1516259762381-22954d7d3ad2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1066&q=80"
      >
        <v-card-title>Signup and Create it</v-card-title>
      </v-img>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field
                ref="name"
                v-model="name"
                :rules="[()=>!!name || '请输入您的名称']"
                label="您的名称"
                :error-messages="errorMessages"
                required
              ></v-text-field>
              <!-- <small class="red--text">未找到已注册邮箱</small> -->
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="您的邮箱"
                ref="email"
                v-model="email"
                :rules="[()=>!!email||'请输入您的邮箱']"
                required
              ></v-text-field>
              <!-- <small class="red--text">未找到已注册邮箱</small> -->
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="您的密码"
                type="password"
                ref="passwd"
                v-model="passwd"
                :rules="[()=>!!passwd||'请输入您的密码']"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="重输密码"
                ref="repasswd"
                v-model="repasswd"
                :rules="[()=>!!repasswd||'请您再次输入密码']"
                type="password"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-autocomplete
                ref="type"
                v-model="type"
                :rules="[() => !!type || '请选择您的用户角色']"
                :items="types"
                label="用户角色"
                required
              ></v-autocomplete>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" @click="submit">确定</v-btn>
        <v-btn color="blue darken-1" text @click="resetForm">取消</v-btn>
        <v-spacer></v-spacer>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    types: ["客户", "项目经理", "开发团队成员", "测试团队成员", "项目负责人"],
    type: null,
    name: null,
    email: null,
    passwd: null,
    repasswd: null,
    formHasErrors: false,
    errorMessages: ""
  }),

  computed: {
    form() {
      return {
        type: this.type,
        name: this.name,
        email: this.email,
        passwd: this.passwd,
        repasswd: this.repasswd
      };
    }
  },

  watch: {
    name() {
      this.errorMessages = "";
    }
  },

  methods: {
    resetForm() {
      this.errorMessages = [];
      this.formHasErrors = false;

      Object.keys(this.form).forEach(f => {
        this.$refs[f].reset();
      });
      this.dialog = false;
    },
    submit() {
      this.formHasErrors = false;

      Object.keys(this.form).forEach(f => {
        if (!this.form[f]) {
          this.formHasErrors = true;
        } else {
          this.dialog = false;
          this.$refs[f].reset();
          window.location.href = "/";
        }
        this.$refs[f].validate(true);
      });
    }
  }
};
</script>

<style>
</style>
