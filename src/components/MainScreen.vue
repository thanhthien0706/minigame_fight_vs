<template>
  <div class="screen">
    <h1>CUỘC CHIẾN GIỮA CÁC VÌ SAO</h1>
    <form class="formInf" action="" @submit.prevent >
      <div class="formInf__box formInf__name">
        <h3>Nhập tên của bạn</h3>
        <input
          type="text"
          class="formInf__name__text"
          placeholder="Tên bạn"
          v-model="infPlayers.name"
        />
      </div>
      <div class="formInf__box formInf__levels">
        <h3>Chọn chế độ chơi</h3>
        <div class="formInf__levels__radio">
          <ul>
            <li>
              <input
                type="radio"
                name="level"
                value="1"
                v-model="infPlayers.level"
                id="easy"
              />
              <label for="easy">Easy</label>
            </li>
            <li>
              <input
                type="radio"
                name="level"
                value="2"
                v-model="infPlayers.level"
                id="normal"
              />
              <label for="normal">Normal</label>
            </li>
            <li>
              <input
                type="radio"
                name="level"
                value="3"
                v-model="infPlayers.level"
                id="hard"
              />
              <label for="hard">Hard</label>
            </li>
            <li>
              <input
                type="radio"
                name="level"
                value="4"
                v-model="infPlayers.level"
                id="superhard"
              />
              <label for="superhard">Super hard</label>
            </li>
          </ul>
        </div>
      </div>
      <input
        type="submit"
        :disabled="!infPlayers.name.length || !infPlayers.level.length"
        name="submitForm"
        value="Vào game"
        @click="onSubmit"
      />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      infPlayers: {
        name: "",
        level: "",
      },
    };
  },
  methods: {
    onSubmit() {
      this.$emit("onStart", { infPlayers: this.infPlayers });
    },
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
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.screen > h1 {
  font-size: 4.5rem;
  text-transform: uppercase;
  color: var(--light);
  text-shadow: 0.1em 0.1em rgba(0, 0, 0, 0.8);
  margin-bottom: 20px;
}

.screen .formInf {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.screen .formInf .formInf__box {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.screen .formInf .formInf__name {
  margin-bottom: 10px;
}

.screen .formInf .formInf__name h3 {
  font-size: 2rem;
  color: var(--light);
  margin-bottom: 5px;
}

.screen .formInf .formInf__name .formInf__name__text {
  width: 250px;
  height: 35px;
  outline: none;
  padding: 5px;
}

.screen .formInf .formInf__levels{
    margin-bottom: 20px;
}

.screen .formInf .formInf__levels h3 {
  font-size: 2rem;
  color: var(--light);
  margin-bottom: 5px;
}

.screen .formInf .formInf__levels .formInf__levels__radio ul{
    list-style-type: none;
    display:  flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
}

.screen .formInf .formInf__levels .formInf__levels__radio ul > li {
    margin-right:  10px;
    font-size: 1.5rem;
}

.screen .formInf .formInf__levels .formInf__levels__radio ul > li label,
.screen .formInf .formInf__levels .formInf__levels__radio ul > li input {
    cursor: pointer;
}

.screen .formInf .formInf__levels .formInf__levels__radio ul > li label{
    color: #c5e9c4;
}

.screen .formInf .formInf__levels .formInf__levels__radio ul > li input{
    margin-right: 5px;
}

.screen .formInf input[name="submitForm"] {
    /* text-align: center; */
    padding: 12px 15px;
    font-size: 1.1rem;
    color: var(--light);
    border-radius: 15px;
    border: 2px solid var(--green);
    background: none;
    transition: 0.3s ease-in-out;
    cursor: pointer;
}

.screen .formInf input[name="submitForm"]:hover {
    background-color: var(--green);
    color: var(--dark);
}

.screen .formInf input[name="submitForm"]:disabled{
    border-color:  rgba(65, 184, 131,0.5);
    color: rgba(243, 243, 243,0.5);   
}

.screen .formInf input[name="submitForm"]:disabled:hover{
    background: none;
    color:rgba(243, 243, 243,0.5) ;
}



</style>
