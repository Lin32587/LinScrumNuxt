<template>
  <v-dialog v-model="dialog" persistent max-width="800px">
    <template v-slot:activator="{ on }">
      <v-btn color="primary" dark v-on="on">创建问题</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="headline">创建问题</span>
      </v-card-title>
      <v-card-text>
        <v-container>
          <v-row>
            <v-col cols="12">
              <v-text-field
                label="问题简述"
                ref="probContent"
                v-model="probContent"
                :rules="[()=>!!probContent||'请输入问题简述']"
                :error-messages="errorMessages"
                required
              ></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-select
                label="问题类型"
                ref="probType"
                v-model="probType"
                :items="probTypeItem"
                :rules="[()=>!!probType||'请输入问题类型']"
                required
              ></v-select>
            </v-col>
            <v-col cols="6">
              <v-select
                label="优先级"
                ref="probPriority"
                v-model="probPriority"
                :items="probPriorityItem"
                :rules="[()=>!!probPriority||'请选择优先级']"
                required
              ></v-select>
            </v-col>
            <v-col cols="12">
              <v-textarea filled ref="probDesc" v-model="probDesc" name="input-7-4" label="问题详情"></v-textarea>
            </v-col>
            <v-col cols="6">
              <v-text-field label="模块" ref="probModule" v-model="probModule"></v-text-field>
            </v-col>
            <v-col cols="6">
              <v-select label="经办人" ref="probDone" :items="probDoneItem" v-model="probDone"></v-select>
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" @click="submit">确定</v-btn>
        <v-btn color="blue darken-1" text @click="resetForm">取消</v-btn>
        <v-snackbar v-model="snackbar" :multi-line="multiLine" :color="primary">
          {{ snacktext }}
          <v-btn color="red" text @click="snackbarClose">关闭</v-btn>
        </v-snackbar>
        <v-spacer></v-spacer>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data: () => ({
    dialog: false,
    multiLine: true,
    color:'',
    snackbar: false,
    snacktext: "创建问题成功",
    errorMessages: "",
    probContent: null,
    probType: "故事",
    probTypeItem: ["故事", "任务", "缺陷"],
    probPriority: "Medium",
    probPriorityItem: ["高", "中", "低"],
    probDone: null,
    probDoneItem: ["林浚镔", "张三", "李四", "王五", "赵六"],
    probDesc: null,
    probModule: null,
    formHasErrors: false
  }),

  computed: {
    form() {
      return {
        probContent: this.probContent,
        probModule: this.probModule,
        probDone: this.probDone,
        // probType: this.probType,
        probDesc: this.probDesc
        // probPriority:this.probPriority,
      };
    }
  },

  watch: {
    probContent() {
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
    snackbarClose() {
      this.snackbar = false;
      this.dialog = false;
      Object.keys(this.form).forEach(f => {
        this.$refs[f].reset();
      });
    },
    submit() {
      this.formHasErrors = false;

      Object.keys(this.form).forEach(f => {
        if (!this.form[f]) this.formHasErrors = true;
        else {
          this.snackbar = true;
          // this.dialog = false;
        }
        this.$refs[f].validate(true);
      });
    }
  }
};
</script>

<style>
</style>
