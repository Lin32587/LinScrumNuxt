<template>
  <v-row justify="center">
    <v-col cols="12">
      <v-card color="grey lighten-4">
        <v-card-title class="grey--text">{{ programname }} 项目</v-card-title>
        <v-card-subtitle class="pb-0">创建时间：{{ Ctime }}</v-card-subtitle>
        <v-row justify="center">
          <v-col cols="12">
            <draggable
              tag="transition-group"
              :componentData="componentData"
              :list="list"
              class="list-group"
              draggable=".item"
              :animation="100"
              @start="dragging = true"
              @end="dragging = false"
            >
              <v-card
                max-height="80px"
                class="list-group-item item ma-2 pa-1"
                v-for="element in list"
                :key="element.name"
                @click="content"
              >
                <v-row justify="left">
                  <v-icon class="pl-4" :color="element.color" v-text="element.icon"></v-icon>
                  <v-card-subtitle v-text="element.id"></v-card-subtitle>
                </v-row>
                <v-card-title class="mt-n8 subtitle-2" v-text="element.name"></v-card-title>
              </v-card>

              <div
                slot="footer"
                class="btn-group list-group-item"
                role="group"
                aria-label="Basic example"
                key="footer"
              >
                <v-col>
                  <!-- <v-btn class="pl-4" @click="add"></v-btn> -->
                  <!-- <createTesk /> -->
                </v-col>
              </div>
            </draggable>
          </v-col>
        </v-row>
      </v-card>

      <rawDisplayer class="col-3" :value="list" title="List" />
    </v-col>
  </v-row>
</template>

<script>
import draggable from "vuedraggable";
import createTesk from "@/components/createTesk";

let id = 1;
export default {
  name: "footerslot",
  display: "Footer slot",
  order: 12,
  components: {
    draggable,
    createTesk
  },
  data() {
    return {
      programname: "MOR",
      Ctime: new Date().toLocaleString(),
      list: [
        { name: "故事", id: 2019121010, icon: "mdi-checkbox-marked",color:"primary" },
        { name: "缺陷", id: 2020022505,icon:"mdi-bomb",color:"red"},
        { name: "任务", id: 2020041108,icon:"mdi-cog-outline",color:"success"},
        { name: "做一个电商网站", id: 2020050108,icon:"mdi-cog-outline",color:"success"}
      ],
      dragging: false,
      componentData: {
        props: {
          type: "transition",
          name: "flip-list"
        }
      }
    };
  },
  methods: {
    add: function() {
      this.list.push({ name: "Juan " + id, id: id++ });
    },
    replace: function() {
      this.list = [{ name: "Edgard", id: id++ }];
    }
  }
};
</script>
<style scoped>
.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}
</style>
