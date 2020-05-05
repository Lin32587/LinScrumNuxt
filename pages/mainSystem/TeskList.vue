<template>
  <v-row justify="center">
    <v-col>
      <v-data-table
        :headers="headers"
        :items="desserts"
        :search="search"
        sort-by="probType"
        class="elevation-4"
      >
        <template v-slot:top>
          <v-toolbar flat>
            <v-toolbar-title class="font-weight-bold">问题清单</v-toolbar-title>
            <v-divider class="mx-4" inset vertical></v-divider>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
            <v-spacer></v-spacer>
            <v-dialog v-model="dialog" max-width="500px">
              <template v-slot:activator="{ on }">
                <v-btn color="primary" dark class="mb-2 font-weight-medium" v-on="on">新增问题</v-btn>
              </template>
              <v-card>
                <v-card-title>
                  <span class="headline">{{ formTitle }}</span>
                </v-card-title>

                <v-card-text>
                  <v-container>
                    <v-row>
                      <v-col cols="12">
                        <v-text-field
                          v-model="editedItem.probContent"
                          label="问题简述"
                          :rules="[()=>!!editedItem.probContent||'请输入问题简述']"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col cols="6">
                        <v-select
                          label="问题类型"
                          v-model="editedItem.probType"
                          :items="probTypeItem"
                          :rules="[()=>!!editedItem.probType||'请输入问题类型']"
                          required
                        ></v-select>
                      </v-col>
                      <v-col cols="6">
                        <v-select
                          label="优先级"
                          v-model="editedItem.probPriority"
                          :items="probPriorityItem"
                          :rules="[()=>!!editedItem.probPriority||'请选择优先级']"
                          required
                        ></v-select>
                      </v-col>
                      <v-col cols="12">
                        <v-textarea filled v-model="editedItem.probDesc" label="预期效果"></v-textarea>
                      </v-col>
                      <v-col cols="6">
                        <v-text-field label="模块" v-model="editedItem.probModule"></v-text-field>
                      </v-col>
                      <v-col cols="6">
                        <v-select label="经办人" :items="probDoneItem" v-model="editedItem.probDone"></v-select>
                      </v-col>
                      <v-col cols="12">
                        <v-menu
                          ref="menu"
                          v-model="menu"
                          :close-on-content-click="false"
                          :return-value.sync="editedItem.probDeadline"
                          transition="scale-transition"
                          offset-y
                          min-width="290px"
                        >
                          <template v-slot:activator="{ on }">
                            <v-text-field
                              v-model="editedItem.probDeadline"
                              label="预期完成时间"
                              readonly
                              v-on="on"
                            ></v-text-field>
                          </template>
                          <v-date-picker v-model="editedItem.probDeadline" no-title scrollable>
                            <v-spacer></v-spacer>
                            <v-btn text color="primary" @click="menu = false">取消</v-btn>
                            <v-btn
                              text
                              color="primary"
                              @click="$refs.menu.save(editedItem.probDeadline)"
                            >确定</v-btn>
                          </v-date-picker>
                        </v-menu>
                      </v-col>
                      <v-col class="d-none">
                        <v-text-field v-model="defaultItem.probCtime" label="创建时间"></v-text-field>
                      </v-col>
                    </v-row>
                  </v-container>
                </v-card-text>

                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" text @click="close">取消</v-btn>
                  <v-btn color="blue darken-1" text @click="save">保存</v-btn>
                </v-card-actions>
              </v-card>
            </v-dialog>
          </v-toolbar>
        </template>
        <template v-slot:item.actions="{ item }">
          <v-icon small class="mr-2" @click="editItem(item)">mdi-pencil</v-icon>
          <v-icon small @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
        <template v-slot:no-data>
          <v-btn color="primary" @click="initialize">Reset</v-btn>
        </template>
      </v-data-table>
    </v-col>
  </v-row>
</template>

<script>
export default {
  layout: "default",
  data: () => ({
    dialog: false,
    menu: false,
    probTypeItem: ["故事", "任务", "缺陷"],
    probPriorityItem: ["高", "中", "低"],
    probDoneItem: ["林浚镔", "张三", "李四", "王五", "赵六"],
    search: "",
    headers: [
      {
        text: "问题简述",
        align: "start",
        sortable: false,
        value: "probContent"
      },
      { text: "问题类型", sortable: false, value: "probType" },
      { text: "优先级", value: "probPriority" },
      { text: "问题详情", sortable: false, value: "probDesc" },
      { text: "所选技术", value: "probTech" },
      { text: "问题状态", value: "probStatu" },
      { text: "所属模块", value: "probModule" },
      { text: "创建时间", value: "probCtime" },
      { text: "预期完成时间", value: "probDeadline" },
      { text: "经办人", value: "probDone" },
      { text: "操作", value: "actions", sortable: false }
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      probContent: "",
      probType: "",
      probPriority: "",
      probDesc: "",
      probTech: "",
      probStatu: "",
      probModule: "",
      probCtime: "",
      probDone: "",
      probDeadline: ""
    },
    defaultItem: {
      probContent: null,
      probType: "故事",
      probPriority: "中",
      probDesc: null,
      probTech: null,
      probStatu: "待办",
      probModule: 0,
      probDone: "",
      probCtime: new Date().toISOString().substr(0, 10),
      probDeadline: new Date().toISOString().substr(0, 10)
    }
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "创建问题" : "编辑问题";
    }
  },

  watch: {
    dialog(val) {
      val || this.close();
    }
  },

  created() {
    this.initialize();
  },

  methods: {
    initialize() {
      this.desserts = [
        {
          probContent: "更新用户管理权限",
          probType: "任务",
          probPriority: "高",
          probDesc: "新增XXX、XXX、XXX用户角色",
          probTech: "Javascript",
          probStatu: "待办",
          probModule: "系统后台管理模块",
          probCtime: 2020 + "-" + "0" + 2 + "-" + 22,
          probDeadline: 2020 + "-" + "0" + 8 + "-" + 28,
          probDone: null
        },
        {
          probContent: "根据用户使用的手机壳更换页面主题",
          probType: "故事",
          probPriority: "中",
          probDesc: null,
          probTech: null,
          probStatu: "待办",
          probModule: null,
          probCtime: 2020 + "-" + "0" + 4 + "-" + 30,
          probDeadline: null,
          probDone: null
        },
        {
          probContent: "为XXX用户添加管理员权限",
          probType: "任务",
          probPriority: "中",
          probDesc: "给张三加上系统超级管理员权限",
          probTech: "Javascrpit、Golang",
          probStatu: "处理中",
          probModule: "系统后台管理模块",
          probCtime: 2019 + "-" + 12 + "-" + 30,
          probDeadline: 2020 + "-" + "0" + 5 + "-" + 23,
          probDone: "林浚镔"
        },
        {
          probContent: "点击XXX按钮之后无法正常跳转页面并会卡死",
          probType: "缺陷",
          probPriority: "高",
          probDesc: null,
          probTech: "Java",
          probStatu: "处理中",
          probModule: null,
          probCtime: 2020 + "-" + "0" + 4 + "-" + 20,
          probDeadline: 2020 + "-" + "0" + 5 + "-" + 15,
          probDone: "李四"
        },
        {
          probContent: "重构XXX页面CSS",
          probType: "故事",
          probPriority: "高",
          probDesc: "重写页面样式表，调整页面配色、UI、配图",
          probTech: "Nuxt、Bootstrap4",
          probStatu: "完成",
          probCtime: 2020 + "-" + "0" + 3 + "-" + 24,
          probDeadline: 2020 + "-" + "0" + 4 + "-" + 10,
          probDone: "林浚镔"
        }
      ];
    },

    editItem(item) {
      this.editedIndex = this.desserts.indexOf(item);
      this.editedItem = Object.assign({}, item);
      this.dialog = true;
    },

    deleteItem(item) {
      const index = this.desserts.indexOf(item);
      confirm("是否确定删除该问题?") && this.desserts.splice(index, 1);
    },

    close() {
      this.dialog = false;
      this.$nextTick(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.editedIndex = -1;
      });
    },

    save() {
      if (this.editedIndex > -1) {
        Object.assign(this.desserts[this.editedIndex], this.editedItem);
      } else {
        this.desserts.push(this.editedItem);
      }
      this.close();
    }
  }
};
</script>

<style>
</style>
