<template>
  <v-container fill-height fluid>
    <v-row>
      <v-col md="6" class="mt-16">
        <router-link :to="{ name: 'Home' }">
          <v-img
            :src="require('../../assets/gophilogodark.png')"
            contain
            height="150"
            class="mt-16"
          />
        </router-link>
        <div class="text-center mt-2">
          <span style="font-size: x-large">
            A subtitling platform for globalizing knowledge
          </span>
        </div>
      </v-col>
      <v-col md="6">
        <v-card height="540" class="mr-9 rounded-xl" flat color="#F1F1F1">
          <v-card-title
            class="justify-center default-color"
            style="font-size: xx-large; font-weight: bolder"
          >
            <span class="mt-5">Welcome to gophi</span>
          </v-card-title>
          <v-row align="center" justify="center" class="mx-7">
            <v-col class="text-center completed-signup">
              <span>Personal Information</span>
            </v-col>
          </v-row>

          <!--Different steps for signing up-->
          <v-window v-model="step">
            <v-window-item :value="1">
              <PersonalInformation></PersonalInformation>
            </v-window-item>

            <v-window-item :value="2">
              <PersonalTwo></PersonalTwo>
            </v-window-item>
          </v-window>

          <v-spacer></v-spacer>
          <v-row> </v-row>
          <v-card-actions class="back-button">
            <v-btn
              color="#13B8A4"
              dark
              rounded
              small
              @click="goBack"
              class="px-6"
            >
              Back
            </v-btn>
          </v-card-actions>
          <v-card-actions class="next-button"
            ><v-btn
              v-if="step < 2"
              color="#13B8A4"
              rounded
              small
              dark
              @click="step++"
              class="px-6 align-content-end"
            >
              Next
            </v-btn>
            <v-btn
              v-else
              color="#13B8A4"
              rounded
              small
              dark
              @click="submitSignup"
              class="px-4 align-content-end"
            >
              Submit
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import PersonalInformation from "./PersonalInformation";
import PersonalTwo from "./PersonalTwo";
export default {
  name: "CustomerSignup",
  components: { PersonalInformation, PersonalTwo },

  data: () => ({
    step: 1,
  }),

  mounted() {
    if (!this.$store.state.refresh || this.$store.state.isLoggedIn) {
      this.$router.push({ name: "Home" });
    }
  },

  beforeMount() {
    window.addEventListener("beforeunload", this.preventNav);
  },

  beforeDestroy() {
    window.removeEventListener("beforeunload", this.preventNav);
  },

  methods: {
    preventNav(event) {
      event.preventDefault();
      event.returnValue = "";
    },

    goBack() {
      if (this.step > 1) {
        this.step--;
      } else {
        this.$router.push({ name: "Login" });
      }
    },
    submitSignup() {
      this.$router.push({ name: "Login" });
    },
  },
};
</script>

<style src="../../css/index.css" />
