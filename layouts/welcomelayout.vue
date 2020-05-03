<template>
  <v-app id="sandbox">
    <!-- <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="primaryDrawer.clipped"
      :floating="primaryDrawer.floating"
      :mini-variant="primaryDrawer.mini"
      :permanent="primaryDrawer.type === 'permanent'"
      :temporary="primaryDrawer.type === 'temporary'"
      app
      overflow
      class="d-none"
    >
      <v-list>
        <v-subheader>REPORTS</v-subheader>
        <v-list-item-group v-model="navitem" color="teal">
          <v-list-item v-for="(navitem, i) in navitems" :key="i">
            <v-list-item-icon>
              <v-icon v-text="navitem.icon"></v-icon>
            </v-list-item-icon>
            <v-list-item-content>
              <v-list-item-title v-text="navitem.text" v-link="navitem.to"></v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer> -->

    <v-app-bar :clipped-left="primaryDrawer.clipped" app>
      <!-- <v-app-bar-nav-icon
        v-if="primaryDrawer.type === 'permanent'"
        @click.stop="primaryDrawer.model = !primaryDrawer.model"
      /> -->

      <div class="row mt-5 mx-auto pl-sm-8">
        <v-toolbar-title class="font-weight-black">LinScrum</v-toolbar-title>

        <!-- <v-switch class="ml-2 pt-1 hidden-sm-and-down" v-model="primaryDrawer.mini" label="Mini" primary /> -->
        <v-switch class="ml-2 pt-1" v-model="$vuetify.theme.dark" primary label="Dark" />
      </div>

      <div class="hidden-sm-and-down text-center">
        <!-- <v-btn flat to="/" exact>Home</v-btn>
        <v-btn flat to="/dndcase" exact>DndCase</v-btn>
        <v-btn flat to="/contact" exact>Contact</v-btn> -->
        <v-btn  color="primary" class="font-weight-regular" dark>登录</v-btn>
        <v-btn text color="teal" class="font-weight-regular" dark>注册</v-btn>
      </div>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-slide-y-transition>
          <v-layout>
            <nuxt />
          </v-layout>
        </v-slide-y-transition>
      </v-container>
    </v-content>

    <!-- <v-content>
      <v-container fluid>
        <v-row
          align="center"
          justify="center"
        >
          <v-col cols="10">
            <v-card>
              <v-card-text>
                <v-row>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Scheme</span>

                  </v-col>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Drawer</span>
                    <v-radio-group
                      v-model="primaryDrawer.type"
                      column
                    >
                      <v-radio
                        v-for="drawer in drawers"
                        :key="drawer"
                        :label="drawer"
                        :value="drawer.toLowerCase()"
                        primary
                      />
                    </v-radio-group>
                    <v-switch
                      v-model="primaryDrawer.clipped"
                      label="Clipped"
                      primary
                    />
                    <v-switch
                      v-model="primaryDrawer.floating"
                      label="Floating"
                      primary
                    />
                    <v-switch
                      v-model="primaryDrawer.mini"
                      label="Mini"
                      primary
                    />
                  </v-col>
                  <v-col
                    cols="12"
                    md="6"
                  >
                    <span>Footer</span>
                    <v-switch
                      v-model="footer.inset"
                      label="Inset"
                      primary
                    />
                  </v-col>
                </v-row>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn text>Cancel</v-btn>
                <v-btn
                  text
                  color="primary"
                >Submit</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>-->

    <v-footer :inset="footer.inset" app>
      <span>Lin</span>
      <span class="px-4">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawers: ["Default (no property)", "Permanent", "Temporary"],
    primaryDrawer: {
      model: null,
      type: "default (no property)",
      clipped: true,
      floating: false,
      mini: true
    },
    // navitem: 1,
    // navitems: [
    //   { text: "Backlog", icon: "mdi-layers" },
    //   { text: "Kanban", icon: "mdi-order-bool-descending-variant" },
    //   { text: "Workflow", icon: "mdi-meteor" },
    //   { text: "Question", icon: "mdi-star-box-multiple" },
    //   { text: "Report", icon: "mdi-trending-up" },
      // { text: "客户需求", icon: "mdi-chart-bubble",to:"/demand"},
      // { text: "产品需求", icon: "mdi-firebase",to:"/demand" },
    // ],
    footer: {
      inset: false
    }
  })
};
</script>
