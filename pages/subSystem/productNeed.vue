<template>
  <v-row justify="center">
    <v-col class="text-center d-sm-none">
      <createTesk />
    </v-col>
    <v-col cols="12">
      <v-data-table
        :headers="headers"
        :items="desserts"
        :search="search"
        sort-by="demandEffect"
        class="elevation-4"
        readonly
      >
        <template v-slot:top>
          <v-toolbar flat>
            <v-toolbar-title class="font-weight-bold">客户需求列表</v-toolbar-title>
            <v-divider class="mx-4" inset vertical></v-divider>
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="Search"
              single-line
              hide-details
            ></v-text-field>
            <v-spacer></v-spacer>
            <!-- <v-dialog v-model="dialog" max-width="500px">
              <template v-slot:activator="{ on }">
                <v-btn color="primary" dark class="mb-2 font-weight-medium" v-on="on">新增需求</v-btn>
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
                          v-model="editedItem.demandContent"
                          label="需求简述"
                          :rules="[()=>!!editedItem.demandContent||'请输入需求简述']"
                          required
                        ></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-text-field v-model="editedItem.demandEffect" label="预期效果"></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="6" md="4">
                        <v-text-field v-model="editedItem.demandTech" label="期望技术"></v-text-field>
                      </v-col>
                      <v-col cols="12" sm="6" md="4">
                        <v-text-field v-model="editedItem.demandPoint" suffix="天" label="交付节点"></v-text-field>
                      </v-col>
                      <v-col cols="12">
                        <v-menu
                          ref="menu"
                          v-model="menu"
                          :close-on-content-click="false"
                          :return-value.sync="editedItem.demandDeadline"
                          transition="scale-transition"
                          offset-y
                          min-width="290px"
                        >
                          <template v-slot:activator="{ on }">
                            <v-text-field
                              v-model="editedItem.demandDeadline"
                              label="预期交付时间"
                              readonly
                              v-on="on"
                            ></v-text-field>
                          </template>
                          <v-date-picker v-model="editedItem.demandDeadline" no-title scrollable>
                            <v-spacer></v-spacer>
                            <v-btn text color="primary" @click="menu = false">取消</v-btn>
                            <v-btn
                              text
                              color="primary"
                              @click="$refs.menu.save(editedItem.demandDeadline)"
                            >确定</v-btn>
                          </v-date-picker>
                        </v-menu>
                      </v-col>
                      <v-col class="d-none">
                        <v-text-field v-model="defaultItem.demandCtime" label="创建时间"></v-text-field>
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
            </v-dialog>-->
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
    <v-col class="text-center d-none d-sm-flex">
      <createTesk />
    </v-col>

  </v-row>
</template>

<script>
import createTesk from "@/components/createTesk"

export default {
  layout: "subLayout",
  components: {
    createTesk,
  },

  data: () => ({
    dialog: false,
    menu: false,
    search: "",
    headers: [
      {
        text: "需求简述",
        align: "start",
        sortable: false,
        value: "demandContent"
      },
      { text: "预期效果", sortable: false, value: "demandEffect" },
      { text: "期望技术", sortable: false, value: "demandTech" },
      { text: "交付节点(天)", value: "demandPoint" },
      { text: "创建时间", value: "demandCtime" },
      { text: "预期交付时间", value: "demandDeadline" }
      // { text: "操作", value: "actions", sortable: false }
    ],
    desserts: [],
    editedIndex: -1,
    editedItem: {
      demandContent: "",
      demandEffect: "",
      demandTech: "",
      demandPoint: "",
      demandCtime: "",
      demandDeadline: ""
    },
    defaultItem: {
      demandContent: null,
      demandEffect: null,
      demandTech: null,
      demandPoint: 0,
      demandCtime: new Date().toISOString().substr(0, 10),
      demandDeadline: new Date().toISOString().substr(0, 10)
    }
  }),

  computed: {
    formTitle() {
      return this.editedIndex === -1 ? "创建需求" : "编辑需求";
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
          demandContent: "修改按钮",
          demandEffect: "“取消”改为“Close”",
          demandTech: "Vue",
          demandPoint: 4,
          demandCtime: 2019 + "-" + 12 + "-" + 25,
          demandDeadline: 2020 + "-" + "0" + 1 + "-" + "0" + 2
        },
        {
          demandContent: "加上一个按钮",
          demandEffect: "点击之后可以跳转到XXX页面",
          demandTech: "Javascript",
          demandPoint: 3,
          demandCtime: 2019 + "-" + 12 + "-" + 31,
          demandDeadline: 2020 + "-" + "0" + 1 + "-" + "0" + 2
        },
        {
          demandContent: "实时改变主题",
          demandEffect: "页面可以根据天气变换色彩",
          demandTech: "Vue,Sass",
          demandPoint: 20,
          demandCtime: 2020 + "-" + "0" + 2 + "-" + "0" + 2,
          demandDeadline: 2020 + "-" + "0" + 2 + "-" + 22
        },
        {
          demandContent: "降低页面加载的延迟",
          demandEffect: "页面加载速度降到0.05s",
          demandTech: "ASP.NET Core",
          demandPoint: 30,
          demandCtime: 2020 + "-" + "0" + 4 + "-" + 20,
          demandDeadline: 2020 + "-" + "0" + 5 + "-" + 20
        },
        {
          demandContent: "做个微信小游戏",
          demandEffect: "能玩就行",
          demandTech: "H5",
          demandPoint: 7,
          demandCtime: 2020 + "-" + "0" + 3 + "-" + 18,
          demandDeadline: 2020 + "-" + "0" + 3 + "-" + 25
        },
        {
          demandContent: "改XXX页面样式，我觉得不好看",
          demandEffect: "字要大，图标要好看，页面要有冲击感",
          demandTech: null,
          demandPoint: 1,
          demandCtime: 2020 + "-" + "0" + 3 + "-" + 20,
          demandDeadline: 2020 + "-" + "0" + 3 + "-" + 21
        },
        {
          demandContent: "做个网上商城",
          demandEffect: "像京东那样",
          demandTech: "JAVA,Angular,MySQL",
          demandPoint: 60,
          demandCtime: 2020 + "-" + "0" + 4 + "-" + 28,
          demandDeadline: null
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
      confirm("是否确定删除该需求?") && this.desserts.splice(index, 1);
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
