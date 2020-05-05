<template>
  <v-container>
    <div class="row text-center">
      <!-- <div class="col-4">
        <h3 class="text-left mb-4">Backlog</h3>
        <v-card class="grey lighten-4" height="100%" :elevation="0">
          <draggable
            id="first"
            data-source="juju"
            :list="list"
            class="pt-2"
            draggable=".item"
            group="a"
          >
            <div class="list-group-item item" v-for="element in list" :key="element.name">
              <v-card :elevation="2" class="ma-2">
                <v-card-subtitle v-text="element.id" class="text-left"></v-card-subtitle>
                <v-card-text v-text="element.name" class="text-left font-weight-black subtitle-1"></v-card-text>
                <v-row justify="left">
                  <v-col cols="4">
                    <v-icon v-text="element.icon" :color="element.color"></v-icon>
                  </v-col>
                  <v-col cols="1">
                    <v-icon v-text="element.picon" :color="element.pcolor"></v-icon>
                  </v-col>
                </v-row>
              </v-card>
            </div>

            <v-card-actions>
              <v-btn @click="add" text>Add</v-btn>
              <v-btn @click="replace" text>Replace</v-btn>
            </v-card-actions>
          </draggable>
        </v-card>
      </div> -->

      <div class="col-4">
        <h3 class="text-left mb-4">待办</h3>
        <v-card class="grey lighten-4" height="100%" :elevation="0">
          <draggable :list="list2" class="list-group pt-2" draggable=".item" group="a">
            <div class="list-group-item item" v-for="element in list2" :key="element.name">
              <v-card :elevation="2" class="ma-2">
                <v-card-subtitle v-text="element.id" class="text-left"></v-card-subtitle>
                <v-card-text v-text="element.name" class="text-left font-weight-black subtitle-1"></v-card-text>
                <v-row justify="left">
                  <v-col cols="4">
                    <v-icon v-text="element.icon" :color="element.color"></v-icon>
                  </v-col>
                  <v-col cols="1">
                    <v-icon v-text="element.picon" :color="element.pcolor"></v-icon>
                  </v-col>
                </v-row>
              </v-card>
            </div>

            <!-- <v-btn-toggle>
            <v-btn @click="add2" depressed>Add</v-btn>
            <v-btn @click="replace2" depressed>Replace</v-btn>
            </v-btn-toggle>-->
          </draggable>
        </v-card>
      </div>

      <div class="col-4">
        <h3 class="text-left mb-4">处理中</h3>
        <v-card class="grey lighten-4" height="100%" :elevation="0">
          <draggable :list="list3" class="list-group pt-2" draggable=".item" group="a">
            <div class="list-group-item item" v-for="element in list3" :key="element.name">
              <v-card :elevation="2" class="ma-2">
                <v-card-subtitle v-text="element.id" class="text-left"></v-card-subtitle>
                <v-card-text v-text="element.name" class="text-left font-weight-black subtitle-1"></v-card-text>
                <v-row justify="left">
                  <v-col cols="4">
                    <v-icon v-text="element.icon" :color="element.color"></v-icon>
                  </v-col>
                  <v-col cols="1">
                    <v-icon v-text="element.picon" :color="element.pcolor"></v-icon>
                  </v-col>
                </v-row>
              </v-card>
            </div>

            <!-- <v-btn-toggle>
            <v-btn @click="add3" depressed>Add</v-btn>
            <v-btn @click="replace3" depressed>Replace</v-btn>
            </v-btn-toggle>-->
          </draggable>
        </v-card>
      </div>

      <div class="col-4">
        <h3 class="text-left mb-4">完成</h3>
        <v-card class="grey lighten-4" height="100%" :elevation="0">
          <draggable :list="list4" class="list-group pt-2" draggable=".item" group="a">
            <div class="list-group-item item" v-for="element in list4" :key="element.name">
              <v-card :elevation="2" class="ma-2">
                <v-card-subtitle v-text="element.id" class="text-left"></v-card-subtitle>
                <v-card-text v-text="element.name" class="text-left font-weight-black subtitle-1"></v-card-text>
                <v-row justify="left">
                  <v-col cols="4">
                    <v-icon v-text="element.icon" :color="element.color"></v-icon>
                  </v-col>
                  <v-col cols="1">
                    <v-icon v-text="element.picon" :color="element.pcolor"></v-icon>
                  </v-col>
                </v-row>
              </v-card>
            </div>

            <!-- <v-btn-toggle>
            <v-btn @click="add4" depressed>Add</v-btn>
            <v-btn @click="replace4" depressed>Replace</v-btn>
            </v-btn-toggle>-->
          </draggable>
        </v-card>
      </div>

      <!-- <rawDisplayer class="col-2" :value="list" title="List" />

      <rawDisplayer class="col-2" :value="list2" title="List2" />-->
    </div>
  </v-container>
</template>

<script>
import draggable from "vuedraggable";
let id = 1;
export default {
  name: "two-list-headerslots",
  display: "Two list header slot",
  order: 14,
  components: {
    draggable
  },
  data() {
    return {
      list: [
        {
          name: "故事",
          id: 2019121010,
          icon: "mdi-checkbox-marked",
          color: "primary",
          picon: "mdi-chevron-double-up",
          pcolor: "red"
        },
        {
          name: "缺陷",
          id: 2020022505,
          icon: "mdi-bomb",
          color: "red",
          picon: "mdi-chevron-double-down",
          pcolor: "success"
        },
        {
          name: "任务",
          id: 2020041108,
          icon: "mdi-cog-outline",
          color: "success",
          picon: "mdi-equal-box",
          pcolor: "yellow darken-4"
        },
        {
          name: "做一个电商网站",
          id: 2020050108,
          icon: "mdi-cog-outline",
          color: "success",
          picon: "mdi-equal-box",
          pcolor: "yellow darken-4"
        }
      ],
      list2: [
        {
          name: "更新用户管理权限",
          id: 2020050109,
          icon: "mdi-cog-outline",
          color: "success",
          picon: "mdi-chevron-double-up",
          pcolor: "red"
        },
        {
          name: "根据用户使用的手机壳更换页面主题",
          id: 2020040818,
          icon: "mdi-checkbox-marked",
          color: "primary",
          picon: "mdi-equal-box",
          pcolor: "yellow darken-4"
        }
      ],
      list3: [
        {
          name: "为XXX用户添加管理员权限",
          id: 2020050907,
          icon: "mdi-cog-outline",
          color: "success",
          picon: "mdi-equal-box",
          pcolor: "yellow darken-4"
        },
        {
          name: "点击XXX按钮之后无法正常跳转页面并会卡死",
          id: 2020010608,
          icon: "mdi-bomb",
          color: "red",
          picon: "mdi-chevron-double-up",
          pcolor: "red"
        }
      ],
      list4: [
        {
          name: "重构XXX页面CSS",
          id: 2019120715,
          icon: "mdi-checkbox-marked",
          color: "primary",
          picon: "mdi-chevron-double-up",
          pcolor:"red"
        }
      ]
    };
  },
  methods: {
    add: function() {
      this.list.push({ name: "Juan " + id, id: id++ });
    },
    replace: function() {
      this.list = [{ name: "Edgard", id: id++ }];
    },
    add2: function() {
      this.list2.push({ name: "Juan " + id, id: id++ });
    },
    replace2: function() {
      this.list2 = [{ name: "Edgard", id: id++ }];
    },
    add3: function() {
      this.list3.push({ name: "Juan " + id, id: id++ });
    },
    replace3: function() {
      this.list3 = [{ name: "Edgard", id: id++ }];
    },
    add4: function() {
      this.list4.push({ name: "Juan " + id, id: id++ });
    },
    replace4: function() {
      this.list4 = [{ name: "Edgard", id: id++ }];
    }
  }
};
</script>
