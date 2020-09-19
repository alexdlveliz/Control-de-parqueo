<template>
  <div class="body">
    <h1>Parqueos</h1>
    <div class="parqueos">
      <div class="sec">
        <div class="parqueo">
          <h1>#1</h1>
          <p>El pokemon es {{ pokemon }}</p>
          <button @click="pruebaPost">reservar</button>
        </div>
        <div class="parqueo">
          <h1>#2</h1>
          <button>reservar</button>
        </div>
      </div>
      <div class="sec"></div>
      <div class="sec">
        <div class="parqueo">
          <h1>#3</h1>
          <button>reservar</button>
        </div>
        <div class="parqueo">
          <h1>#4</h1>
          <button>reservar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Parqueos",
  data() {
    return {
      pokemon: "",
    };
  },
  methods: {
    async pruebaGet() {
      const getPokemon = await fetch("https://pokeapi.co/api/v2/pokemon/12/")
        .then((res) => res.json())
        .catch((err) => console.log(err));
      this.pokemon = getPokemon.name;
    },
    async pruebaPost() {
      var raw =
        '[\n    {\n        "position": 1,\n        "taken": false\n    }\n]';

      var requestOptions = {
        method: "POST",
        body: raw,
        redirect: "follow",
      };

      fetch("http://localhost:3000/parking", requestOptions)
        .then((response) => response.text())
        .then((result) => console.log(result))
        .catch((error) => console.log("error", error));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.body {
  margin: 0px;
  padding: 25px;
  background-color: blueviolet;
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
}
.parqueos {
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 80vw;
  height: 60%;
  padding: 25px;
  margin: 20px;
  background-color: cornsilk;
  border-radius: 15px;
}
.sec {
  display: flex;
  width: 80vw;
  height: 80%;
  flex-direction: column;
  align-content: space-between;
  align-items: center;
}
.parqueo {
  display: flex;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 50%;
  height: 55%;
  padding: 25px;
  margin: 20px;
  background-color: black;
  color: purple;
  border-radius: 15px;
}
</style>
