<template>
  <div>
    <div>
      <v-app-bar color="#191919" dark x-small>
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <div class="d-flex align-center" style="cursor: pointer" @click="goToDashboard()">
          <img src="../../assets/logo.png" class="logo" />
          <label class="text-h5">
            Banana Reader
          </label>
        </div>
        <v-spacer></v-spacer>

        <HeaderBarLinks></HeaderBarLinks>
      </v-app-bar>

      <v-navigation-drawer
        v-model="drawer"
        absolute
        top
        temporary
        src="https://i.pinimg.com/originals/2a/c5/8c/2ac58ca3c5e1d553148f12ba1d7a38e8.jpg"
      >
        <v-list>
          <v-list-item class="px-2"> </v-list-item>

          <v-list-item link>
            <v-list-item-content>
              <v-list-item-title class="text-h5" style="color:#fff">
                Banana Reader
              </v-list-item-title>
              <v-list-item-title class="text-h6" style="color:#fff">
              </v-list-item-title>
              <v-list-item-subtitle> </v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
        </v-list>

        <v-divider></v-divider>
        <v-list nav dense>
          <v-list-item-group
            v-model="group"
            active-class="deep-purple--text text--accent-4"
          >
            <v-list-item
              v-for="item in items"
              :key="item.title"
              @click="item.action"
              link
            >
              <v-list-item-icon>
                <v-icon style="color:#fff">{{ item.icon }}</v-icon>
              </v-list-item-icon>

              <v-list-item-content>
                <v-list-item-title style="color:#fff">{{
                  item.title
                }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>
    </div>
  </div>
</template>

<script>
import HeaderBarLinks from "./HeaderBarLinks";
export default {
  name: "Menu",
  components: {
    HeaderBarLinks,
  },
  data() {
    return {
      user: JSON.parse(localStorage.getItem("user")),
      drawer: false,
      group: null,
      modal: false,
      inProcess: false,
      appointmentList: [],
      todos: [],
      headers: [
        { text: "Fecha", align: "start", sortable: false, value: "date" },
        { text: "Hora", value: "hour", sortable: false },
        { text: "Tipo", value: "Tipos", sortable: false },
        { text: "Genero", value: "Genero", sortable: false },
        { text: "Actions", value: "actions", sortable: false },
      ],
      items: [
        {
          title: "Dashboard",
          icon: "mdi-home",
          rol: ["admin", "Cliente", "Tailor"],
          action: this.goToDashboard,
        },
        {
          title: "SOAP",
          icon: "mdi-account-box",
          action: this.goToSOAP,
        }, 
      ],
      messages: 1,
    };
  },
  methods: {
    close() {
      this.modal = false;
    },
    showModal() {
      this.modal = true;
    },
    closeModal() {
      this.modal = false;
    },
    goToDashboard() {
      return this.$router.push("/");
    },
      goToSOAP(){
        return this.$router.push("/soap");
      },
  },
  mounted() {
    this.user = JSON.parse(localStorage.getItem("user"));
  },
  created() {
    this.user = JSON.parse(localStorage.getItem("user"));
  },
};
</script>

<style>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background: #ffffff;
  width: 500px;
  height: 250px;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
  justify-content: flex-end;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}
.logo {
  width: 40px;
  height: auto;
}
</style>
