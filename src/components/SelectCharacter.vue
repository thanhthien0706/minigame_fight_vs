<template>
  <div class="screen">
    <h1>Chọn Nhân Vật của bạn</h1>

    <div class="showCharacter">
      <img
        :src="`${require('@/assets/images/' + this.isImage + '.png')}`"
        alt=""
      />
      <h3 class="name_character_show">{{ isName }}</h3>
      <div class="boxSkill">
        <ul>
          <li
            :style="{
              backgroundImage: `url(${require('@/assets/images/avt_' +
                this.isImage +
                '-1.png')})`,
            }"
          ></li>
          <li
            :style="{
              backgroundImage: `url(${require('@/assets/images/avt_' +
                this.isImage +
                '-2.png')})`,
            }"
          ></li>
          <li
            :style="{
              backgroundImage: `url(${require('@/assets/images/avt_' +
                this.isImage +
                '-3.png')})`,
            }"
          ></li>
        </ul>
      </div>
    </div>

    <div class="box_characters" ref="characterMain">
      <card
        v-for="character in characters"
        :key="character.id"
        :idCharacter="character.id"
        :nameCharacter="character.name"
        :ref="`cart_${character.id}`"
        @onShowCharacter="showCharacter($event)"
      />
    </div>

    <div class="box_enter_game">
      <button class="btn_enter_game" :disabled="!character.length" @click="onClickGetCharacter">Chọn</button>
    </div>
  </div>
</template>

<script>
import Card from "./Cart.vue";

import { randonFunction } from "../utils/random";

export default {
  components: {
    Card,
  },
  data() {
    return {
      characters: [
        {
          id: 1,
          name: "Batman",
        },
        {
          id: 2,
          name: "KhaBanh's",
        },
        {
          id: 3,
          name: "Songoku",
        },
        {
          id: 4,
          name: "Superman",
        },
        {
          id: 5,
          name: "trandan's",
        },
      ],
      bot:{
          idCharacter : "",
          nameCharacter : "",
      },
      character: [],
      isImage: 0,
      isName: "",
    };
  },
  methods: {
    showCharacter(card) {
      if (this.character.length === 0) {
        this.character.push(card);
        this.$refs[`cart_${this.character[0].idCharacterNew}`].onAddActive();
        this.isImage = this.character[0].idCharacterNew;
        this.isName = this.character[0].nameCharacterNew;
        return false;
      }
      if (
        this.character.length === 1 &&
        this.character[0].idCharacterNew == card.idCharacterNew
      ) {
        this.$refs[`cart_${this.character[0].idCharacterNew}`].onRemoveActive();
        this.character = [];
        this.isImage = 0;
        this.isName = "";
      }
      if (
        this.character.length === 1 &&
        this.character[0].idCharacterNew != card.idCharacterNew
      ) {

        this.$refs[`cart_${this.character[0].idCharacterNew}`].onRemoveActive();
        this.$refs[`cart_${card.idCharacterNew}`].onAddActive();
        this.character[0] = card;
        this.isImage = this.character[0].idCharacterNew;
        this.isName = this.character[0].nameCharacterNew;
      }
    },
    onClickGetCharacter(){
        const randomBot = Math.round(randonFunction(0, this.characters.length-1));

        this.bot.idCharacter = this.characters[randomBot].id;
        this.bot.nameCharacter = this.characters[randomBot].name;

        this.$emit('onGetCharacter', {infCharacter: this.character[0] , infBot: this.bot});
    }
  },
};
</script>

<style lang="css" scoped>
.screen {
  max-width: 1020px;
  width: 100%;
  margin: 0 auto;
  height: 100vh;
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.screen h1 {
  text-transform: uppercase;
  font-size: 3rem;
  color: var(--light);
}

.box_characters {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-left: -20px;
  margin-right: -20px;
  margin-bottom: 15px;
}

.showCharacter {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-bottom: 20px;
}

.showCharacter img {
  width: 100%;
  height: 320px;
  object-fit: cover;
  margin-bottom: 10px;
}

.showCharacter .name_character_show {
  font-size: 1.7rem;
  color: var(--light);
  margin-bottom: 10px;
}
.showCharacter .boxSkill ul {
  list-style-type: none;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.showCharacter .boxSkill ul > li {
  background-repeat: no-repeat;
  background-size: contain;
  background-position: center;
  height: 50px;
  width: 50px;
  margin: 0 15px;
  padding: 7px;
  background-color: var(--green);
  border-radius: 50%;
}

.box_enter_game .btn_enter_game {
  width: 100px;
  height: 40px;
  background-color: var(--green);
  font-size: 1.2rem;
  color: var(--light);
  outline: none;
}

.box_enter_game .btn_enter_game:disabled {
  opacity: 0.8;
}
</style>
