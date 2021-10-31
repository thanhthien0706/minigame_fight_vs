<template>
  <main-screen
    @onStart="onHandleBeforeStart($event)"
    v-if="statusMatch == 'default'"
  />
  <select-character v-if="statusMatch == 'selectCharacter'" />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import SelectCharacter from "./components/SelectCharacter.vue";
export default {
  name: "App",
  components: {
    MainScreen,
    SelectCharacter,
  },
  data() {
    return {
      settings: {
        userName: "",
        levelUser: "",
      },
      statusMatch: "default",
    };
  },
  methods: {
    onHandleBeforeStart(event) {
      this.settings.userName = event.infPlayers.name;
      this.settings.levelUser = event.infPlayers.level;
      this.statusMatch = "selectCharacter";
    },
  },
};
</script>

<style></style>
