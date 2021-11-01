<template>
  <div class="screen">
    <div class="modal_startGame" :class="{ active: startGame }">
      <p class="number__countdown">{{ timeStart }}</p>
    </div>

    <div class="row">
      <div class="col-half">
        <div class="box_header">
          <p class="">{{ infPlayersSettings.userName }}</p>
          <div
            class="healthBar"
            :style="{ width: player.userHeart + '%' }"
          ></div>
        </div>
      </div>

      <div class="box_time">
        <p class="setTimeClock">{{ timeClock }}</p>
      </div>

      <div class="col-half">
        <div class="box_header" style="text-align: right">
          <p class="">{{ infBotSettings.botName }}</p>
          <div
            class="healthBar float-right"
            :style="{ width: bot.botHeart + '%' }"
          ></div>
        </div>
      </div>
    </div>

    <div class="row rowShowCharacter">
      <div class="col-6">
        <div class="box_character text-align-left">
          <img
            class=""
            :src="`${require('@/assets/images/' +
              infPlayersSettings.idCharacter +
              '.png')}`"
            alt=""
          />
        </div>

        <div class="boxSkill">
          <ul
            class="justify-content-left"
            :class="`${this.hits % 2 != 0 ? 'active' : ''}`"
          >
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infPlayersSettings.idCharacter +
                  '-1.png')})`,
              }"
              @click="onStartSkill(1)"
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infPlayersSettings.idCharacter +
                  '-2.png')})`,
              }"
              @click="onStartSkill(2)"
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infPlayersSettings.idCharacter +
                  '-3.png')})`,
              }"
              @click="onStartSkill(3)"
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/sk_4.png')})`,
              }"
              @click="onStartSkill(4)"
            ></li>
          </ul>
        </div>

        <div class="box_notification">
          <p>{{ player.notification }}</p>
        </div>
      </div>

      <div class="col-6">
        <div class="box_character text-align-right">
          <img
            class=""
            :src="`${require('@/assets/images/' +
              infBotSettings.idCharacter +
              '.png')}`"
            alt=""
          />
        </div>

        <div class="boxSkill">
          <ul
            class="justify-content-right"
            :class="`${this.hits % 2 == 0 ? 'active' : ''}`"
          >
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infBotSettings.idCharacter +
                  '-1.png')})`,
              }"
              disabled
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infBotSettings.idCharacter +
                  '-2.png')})`,
              }"
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/avt_' +
                  infBotSettings.idCharacter +
                  '-3.png')})`,
              }"
            ></li>
            <li
              :style="{
                backgroundImage: `url(${require('@/assets/images/sk_4.png')})`,
              }"
            ></li>
          </ul>
        </div>

        <div class="box_notification">
          <p>{{ bot.notification }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { randonFunction } from "../utils/random";

export default {
  props: {
    infPlayersSettings: {
      type: Object,
    },
    infBotSettings: {
      type: Object,
    },
    setlevel: [String, Number],
    startGame: Boolean,
    timeStart: Number,
  },
  data() {
    return {
      selecLevel: this.level,
      player: {
        userHeart: 100,
        notification: "",
      },
      bot: {
        botHeart: 100,
        notification: "",
      },
      timeClock: "00:00",
      hits: 0,
      winer: {
        name: "",
      },
    };
  },
  methods: {
    onTimeClock() {
      let minute = 0;
      let second = 0;
      setInterval(() => {
        second++;
        if (second < 10 && minute < 10) {
          this.timeClock = "0" + minute + ":0" + second;
        }
        if (second >= 10 && minute < 10) {
          this.timeClock = "0" + minute + ":" + second;
        }
        if (second == 60) {
          minute++;
          second = 0;
        }
        if (second < 10 && minute >= 10) {
          this.timeClock = minute + ":0" + second;
        }
        if (second >= 10 && minute >= 10) {
          this.timeClock = minute + ":" + second;
        }
        if (second == 60) {
          minute++;
          second = 0;
        }
        if (minute == 60) {
          minute = 0;
        }
      }, 1000);
    },
    onStartSkill(numberSkill) {
      if (this.hits % 2 == 0) {
        if (numberSkill == 2) {
          this.onMinusBloodBot(this.randomDamage(4, 6));
          this.hits++;
          if (this.bot.botHeart > 0) {
            setTimeout(() => {
              this.onMinusBloodPlayer(this.randomDamage(4, 6));
              this.hits++;
            }, 2000);
          }
        }

        if (numberSkill == 3) {
          this.onMinusBloodBot(this.randomDamage(10, 15));
          this.hits++;
          if (this.bot.botHeart > 0) {
            setTimeout(() => {
              this.onMinusBloodPlayer(this.randomDamage(10, 15));
              this.hits++;
            }, 500);
          }
        }

        if (numberSkill == 4) {
          this.onPlusBlood(this.randomDamage(10, 15));
          this.hits++;
          setTimeout(() => {
            this.onMinusBloodPlayer(this.randomDamage(10, 15));
            this.hits++;
          }, 2000);
        }
      } else {
        return false;
      }
    },

    onPlusBlood(blood) {
      // if (this.hits % 2 != 0) {
      if (this.player.userHeart >= 100) {
        return false;
      } else {
        this.player.userHeart += blood;
        if (this.player.userHeart >= 100) {
          this.player.userHeart = 100;
        }
      }
      // }
    },

    onMinusBloodBot(damage) {
      this.bot.botHeart -= damage;
      // if (this.hits % 2 == 0) {
      if (this.bot.botHeart <= 0) {
        this.winer.name = this.infPlayersSettings.userName;
        this.bot.botHeart = 0;
        setTimeout(() => {
          this.endGame();
        }, 2000);
        return false;
      }
    },

    onMinusBloodPlayer(damage) {
      this.player.userHeart -= damage;

      if (this.player.userHeart <= 0) {
        this.winer.name = this.infBotSettings.botName;
        this.player.userHeart = 0;
        // setTimeout(() => {
        this.endGame();
        // },2000)
        return false;
      }
    },

    endGame() {
      this.$emit("onEndGame", {
        infWiner: this.winer,
        timeGame: this.timeClock,
      });
    },

    randomDamage(da1, da2) {
      let damage = 0;
      if (this.checkLevel(1)) {
        let nda1 = da1 + 2;
        let nda2 = da2 + 5;
        damage = Math.round(randonFunction(nda1, nda2));
      }
      if (this.checkLevel(2)) {
        let nda1 = da1 + 5;
        let nda2 = da2 + 7;
        damage = Math.round(randonFunction(nda1, nda2));
      }
      if (this.checkLevel(3)) {
        let nda1 = da1 + 7;
        let nda2 = da2 + 10;
        if (this.hits % 2 == 4) {
          nda1 += 5;
          nda2 += 10;
        }
        if ((this.hits - 1) % 2 == 4) {
          nda1 += 6;
          nda2 += 12;
        }
        damage = Math.round(randonFunction(nda1, nda2));
      }
      if (this.checkLevel(4)) {
        let nda1 = da1 + 10;
        let nda2 = da2 + 13;
        if (this.hits % 2 == 3) {
          nda1 += 6;
          nda2 += 12;
        }
        if ((this.hits - 1) % 2 == 3) {
          nda1 += 7;
          nda2 += 14;
        }
        damage = Math.round(randonFunction(nda1, nda2));
      }
      return damage;
    },
    checkLevel(numberLevel) {
      if (numberLevel == this.setlevel) {
        return true;
      }
      return false;
    },
  },
  watch: {
    startGame() {
      this.onTimeClock();
    },
  },
};
</script>

<style lang="css" scoped>
@keyframes scaleText {
  from {
    opacity: 1;
    transform: translate(-50%, -50%) scale(0);
  }
  to {
    opacity: 0;
    font-size: 10rem;
    transform: translate(-50%, -50%) scale(2);
  }
}

.screen {
  max-width: 1020px;
  width: 100%;
  margin: 0 auto;
  position: relative;
}

.modal_startGame.active {
  position: fixed;
  z-index: 222;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
}
.modal_startGame .number__countdown {
  display: none;
}

.modal_startGame.active .number__countdown {
  display: block;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-size: 4rem;
  color: var(--light);
  animation: scaleText 1s ease-out infinite;
}

.screen .row {
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  margin-right: -15px;
  margin-left: -15px;
  align-items: center;
}

.col-half {
  position: relative;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  -ms-flex: 0 0 50%;
  flex: 0 0 40%;
  max-width: 40%;
}

.col-6 {
  position: relative;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  -ms-flex: 0 0 50%;
  flex: 0 0 50%;
  max-width: 50%;
}

.box_time {
  position: relative;
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  -ms-flex: 0 0 50%;
  flex: 0 0 20%;
  max-width: 20%;
}

.box_header p {
  color: var(--light);
  margin-bottom: 5px;
  font-size: 1.5rem;
}

.box_header .healthBar {
  background-color: var(--light);
  height: 20px;
  clip-path: polygon(0 0, 95% 0, 100% 100%, 20px 100%);
  background-color: var(--green);
  transition: 0.5s ease-out;
}

.box_time {
}

.box_time .setTimeClock {
  text-align: center;
  font-size: 3rem;
  font-weight: bold;
  color: var(--light);
}

.rowShowCharacter .box_character {
  /* text-align: center; */
  margin-top: 100px;
  margin-bottom: 20px;
}

.rowShowCharacter .box_character img {
  width: auto;
  height: 400px;
}

.boxSkill ul {
  list-style-type: none;
  display: flex;
  flex-direction: row;
  /* justify-content: center; */
  align-items: center;
}

.boxSkill ul.active > li {
  opacity: 0.5;
}

.boxSkill ul > li {
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  height: 50px;
  width: 50px;
  margin: 0 15px;
  padding: 7px;
  background-color: var(--green);
  border-radius: 50%;
  cursor: pointer;
  transition: 0.5s ease-out;
}

.boxSkill ul > li:hover {
  opacity: 0.7;
}

.boxSkill ul.active > li:hover {
  opacity: 0.5;
}
</style>
