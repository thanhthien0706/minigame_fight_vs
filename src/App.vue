<template>
  <main-screen
    @onStart="onHandleBeforeStart($event)"
    v-if="statusMatch == 'default'"
  />
  <select-character
    v-if="statusMatch == 'selectCharacter'"
    @onGetCharacter="onCharacter($event)"
  />

  <attack-screen
    v-if="statusMatch == 'attack'"
    :infPlayersSettings="settingsPlayer"
    :infBotSettings="settingsBot"
    :setlevel="islevel"
    :startGame="startGameSet"
    :timeStart="timeStartGame"
    @onEndGame="callEndGameScreen($event)"
  />

  <end-game-screen
    v-if="statusMatch == 'endGame'"
    :infShowEndGame="infPlayerEndGame"
    @onStartAgain="onAgainGame"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import SelectCharacter from "./components/SelectCharacter.vue";
import AttackScreen from "./components/AttackScreen.vue";
import EndGameScreen from "./components/EndGameScreen.vue";

export default {
  name: "App",
  components: {
    MainScreen,
    SelectCharacter,
    AttackScreen,
    EndGameScreen,
  },
  data() {
    return {
      settingsPlayer: {
        userName: "",
        // levelUser: "",
        idCharacter: "",
        nameCharacter: "",
        userHeart: 100,
      },
      settingsBot: {
        botName: "I am a bot",
        // levelBot: "",
        idCharacter: "",
        nameCharacter: "",
        botHeart: 100,
      },
      statusMatch: "default",
      islevel: 0,
      startGameSet: true,
      timeStartGame: 3,
      infPlayerEndGame: {
        name: "",
        timeEndGame: "",
      },
    };
  },
  methods: {
    onHandleBeforeStart(event) {
      this.settingsPlayer.userName = event.infPlayers.name;
      // this.settingsPlayer.levelUser = event.infPlayers.level;
      this.islevel = event.infPlayers.level;

      // this.settingsBot.levelBot = event.infPlayers.level;

      this.statusMatch = "selectCharacter";
    },
    onCharacter(event) {
      this.settingsPlayer.idCharacter = event.infCharacter.idCharacterNew;
      this.settingsPlayer.nameCharacter = event.infCharacter.nameCharacterNew;

      this.settingsBot.idCharacter = event.infBot.idCharacter;
      this.settingsBot.nameCharacter = event.infBot.nameCharacter;

      this.statusMatch = "attack";
      setTimeout(() => {
        this.startGameSet = false;
      }, 3000);
      let timeCountDown = setInterval(() => {
        this.timeStartGame--;
        if (this.timeStartGame <= 0) {
          clearInterval(timeCountDown);
        }
      }, 1000);
    },
    callEndGameScreen(event) {
      this.infPlayerEndGame.name = event.infWiner.name;
      this.infPlayerEndGame.timeEndGame = event.timeGame;
      this.statusMatch = "endGame";
    },
    onAgainGame() {
      this.statusMatch = "default";
    },
  },
};
</script>

<style></style>
