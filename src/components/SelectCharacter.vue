<template>
  <div class="screen">
    <h1>Chọn Nhân Vật của bạn</h1>
    <div class="box_characters">
      <card
        v-for="character in characters"
        :key="character.id"
        :idCharacter="character.id"
        :nameCharacter="character.name"
      />
    </div>
  </div>
</template>

<script>
import Card from "./Cart.vue";
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
    };
  },
};
</script>

<style lang="css" scoped>
.screen{
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
    margin-bottom: 25px;
    text-transform: uppercase;
    font-size: 4rem;
    color: var(--light) ;
}

.box_characters{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-left: -20px;
    margin-right: -20px;
}
</style>
