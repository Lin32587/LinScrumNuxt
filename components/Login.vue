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
              <v-text-field
                label="用户名或邮箱"
                ref="nameemail"
                v-model="nameemail"
                :rules="[()=>!!nameemail||'请输入用户名或邮箱']"
                :error-messages="errorMessages"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                label="用户密码"
                type="password"
                ref="passwd"
                v-model="passwd"
                :rules="[()=>!!passwd||'请输入用户密码']"
                required
              ></v-text-field>
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
    errorMessages: "",
    nameemail: null,
    passwd: null,
    formHasErrors: false
  }),

  computed: {
    form() {
      return {
        nameemail: this.nameemail,
        passwd: this.passwd
      };
    }
  },

  watch: {
    nameemail() {
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
      if (this.nameemail == "Lin") {
        window.location.href = "/subSystem/clientNeed";
      } else if (this.nameemail == "PM") {
        window.location.href = "/subSystem/productNeed";
      } else if (this.nameemail == "team") {
        window.location.href = "/mainSystem/Backlog";
      }
      Object.keys(this.form).forEach(f => {
        if (!this.form[f]) this.formHasErrors = true;
        else {
          this.dialog = false;
          this.$refs[f].reset();
        }
        this.$refs[f].validate(true);
      });
    }
  }
};
</script>

<style>
</style>
