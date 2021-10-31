<template>
  <div class="screenCart">
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
      style: Number,
    },
    nameCharacter: {
      type: String,
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
  background-color: rgba(0,0,0,0.5);
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
