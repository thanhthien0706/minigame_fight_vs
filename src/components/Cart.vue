<template>
  <div
    class="screenCart"
    :class="{ active: isActive }"
    @click="onClickActive(idCharacter, nameCharacter)"
  >
    <div class="item_character">
      <div
        class="box_image_character"
        :style="{
          backgroundImage: `url(${require('@/assets/images/' +
            idCharacter +
            '.png')})`,
        }"
      ></div>
      <p class="text_name_character">{{ nameCharacter }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    idCharacter: {
      type: Number,
    },
    nameCharacter: {
      type: String,
    },
  },
  data() {
    return {
      isActive: false,
      selectCharacter: [],
    };
  },
  methods: {
    onClickActive(id, name) {
      // console.log(id, name);
      this.$emit("onShowCharacter", {
        idCharacterNew: id,
        nameCharacterNew: name,
      });
    },
    onRemoveActive() {
      this.isActive = false;
    },
    onAddActive() {
      this.isActive = true;
    },
  },
};
</script>

<style lang="css" scoped>
@keyframes rotate {
  100% {
    transform: rotate(1turn);
  }
}

.screenCart {
  padding-right: 20px;
  padding-left: 20px;
  clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%);
  background-color: rgba(0, 0, 0, 0.5);
  position: relative;
  transition: 0.5s ease-out;
}

.screenCart::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 0;
  height: 5px;
  background-color: var(--green);
  transition: 0.5s ease-out;
}

.screenCart:hover::after {
  width: 100%;
}

.screenCart:hover {
  cursor: pointer;
  box-shadow: inset 11px -7px 20px #fff;
}

.screenCart.active {
  box-shadow: inset 11px -7px 20px #fff;
}

.screenCart.active::after {
  width: 100%;
}

.item_character {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 150px;
  height: 150px;
}

.box_image_character {
  width: 100px;
  height: 100px;
  background-position: center center;
  background-repeat: no-repeat;
  background-size: contain;
  margin-bottom: 10px;
}
.text_name_character {
  font-size: 1.2rem;
  color: var(--light);
}
</style>
