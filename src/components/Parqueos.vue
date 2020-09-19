<template>
  <div class="body">
    <h1>Parqueos</h1>
    <div class="parqueos">
      <div class="sec">
        <div class="parqueo">
          <h2># 1</h2>
          <button class="button type1" @click="getInfo">RESERVAR</button>
        </div>
        <div class="parqueo">
          <h2># 2</h2>
          <button class="button type1">RESERVAR</button>
        </div>
      </div>
      <div class="sec">
        <div class="parqueo">
          <h2># 3</h2>
          <button class="button type1">RESERVAR</button>
        </div>
        <div class="parqueo">
          <h2># 4</h2>
          <button class="button type1">RESERVAR</button>
        </div>
      </div>
    </div>
    <h1>Estadisticas</h1>
    <div class="parqueos"></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Parqueos",
  data() {
    return {
      info: "",
    };
  },
  methods: {
    getInfo() {
      var config = {
        method: "get",
        url: "http://localhost:3000/parking",
        headers: {},
        data: "",
      };

      axios(config)
        .then(function(response) {
          console.log(JSON.stringify(response.data));
        })
        .catch(function(error) {
          console.log(error);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Acme&family=Fredoka+One&family=Righteous&display=swap");
.body {
  margin: 0;
  padding: 10px;
  background: #1b4965;
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.body h1 {
  color: beige;
  font-size: 75px;
  font-family: "Righteous", cursive;
}
.parqueos {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 80vw;
  height: 63%;
  padding: 15px;
  margin: 20px;
  background-color: #f4f3ee;
  border-radius: 15px;
}
.sec {
  display: flex;
  position: relative;
  width: 80vw;
  height: 70%;
  flex-direction: column;
  align-content: flex-start;
  align-items: center;
}
.parqueo {
  display: flex;
  position: relative;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 60%;
  height: 55%;
  padding: 25px;
  margin: 20px;
  background-color: #cae9ff;
  border-radius: 15px;
}
.parqueo h2 {
  color: #1b4965;
  font-family: "Fredoka One", cursive;
  font-size: 40px;
}
.button {
  position: relative;
  border: none;
  padding: 1em 1.5em;
  background-color: transparent;
  cursor: pointer;
  outline: 0;
  font-size: 12px;
  font-weight: bold;
}
.button.type1 {
  color: #566473;
}
.button.type1.type1::after,
.button.type1.type1::before {
  content: "";
  display: block;
  position: absolute;
  width: 20%;
  height: 20%;
  border: 2px solid;
  transition: all 0.6s ease;
  border-radius: 2px;
}
.button.type1.type1::after {
  bottom: 0;
  right: 0;
  border-color: transparent #566473 #566473 transparent;
}
.button.type1.type1::before {
  top: 0;
  left: 0;
  border-color: #566473 transparent transparent #566473;
}
.button.type1.type1:hover:after,
.button.type1.type1:hover:before {
  width: 100%;
  height: 100%;
}
.estadisticas {
  width: 100%;
  height: 750px;
  padding: 25px;
  background-color: cornsilk;
}
.estadisticas h1 {
  color: #1b4965;
}
</style>
