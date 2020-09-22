<template>
  <div class="body">
    <h1>Parqueos</h1>
    <div class="parqueos">
      <button @click="getData">Refrescar</button>
      <div class="sec">
        <div :class="{ parqueo: parqueo1 == false, parqueo_ocupado: parqueo1 == true }">
          <h2># 1</h2>
          <button class="button type1" @click="reservar(1)">RESERVAR</button>
        </div>
        <div :class="{ parqueo: parqueo2 == false, parqueo_ocupado: parqueo2 == true }">
          <h2># 2</h2>
          <button class="button type1" @click="reservar(2)">RESERVAR</button>
        </div>
      </div>
      <div class="sec">
        <div :class="{ parqueo: parqueo3 == false, parqueo_ocupado: parqueo3 == true }">
          <h2># 3</h2>
          <button class="button type1" @click="reservar(3)">RESERVAR</button>
        </div>
        <div :class="{ parqueo: parqueo4 == false, parqueo_ocupado: parqueo4 == true }">
          <h2># 4</h2>
          <button class="button type1" @click="reservar(4)">RESERVAR</button>
        </div>
      </div>
    </div>
    <h1>Estadísticas</h1>
    <div class="parqueos"></div>
  </div>
</template>

<script>

export default {
  name: "Parqueos",
  data() {
    return {
      data: "",
      parqueo1: false,
      parqueo2: false,
      parqueo3: true,
      parqueo4: true
    };
  },
  methods: {
    async getData() {
      // Llamada a la API para obtener parqueos
      let data = await fetch("http://localhost:3000/parking")
        .then((res) => res.json());
      this.data = data;
      // console.log(this.data[0].record[this.data[0].record.length - 1].taken);
      this.parqueo1 = this.data[0].record[this.data[0].record.length - 1].taken;
      this.parqueo2 = this.data[1].record[this.data[1].record.length - 1].taken;
      this.parqueo3 = this.data[2].record[this.data[2].record.length - 1].taken;
      this.parqueo4 = this.data[3].record[this.data[3].record.length - 1].taken;
      console.log("actualizado");
    },
    ciclo() {
      let interval = setInterval(async function () {
        let cont = 10;
        cont--;
        let data = await fetch("http://localhost:3000/parking")
          .then((res) => res.json());
        this.data = data;

        for (let i = 0; i < this.data.length; i++) {
          this.info[i] = this.data[i].record[this.data[i].record.length - 1].taken;
        }
        if (cont < 1) {
          clearInterval(interval);
        }
      }, 10000);
    },
    async reservar(position) {
      // Preparación de datos
      let id = this.data[position - 1].id;
      var raw = `{
          "position": ${position},
          "record": [
            {
              "taken": true
            }
          ]
        }`;
      var requestOptions = {
        method: "PUT",
        headers: {
          'Content-Type': 'application/json'
        },
        body: raw,
        redirect: "follow"
      };

      // Llamada a la API para actualizar
      fetch(`http://localhost:3000/parking/${id}`, requestOptions)
        .then((response) => response.text())
        .then((result) => console.log(result))
        .then(() => this.getData())
        .catch((error) => console.log("error", error));
    },
  },
  created() {
    this.getData();
    // this.ciclo();
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

.parqueo_ocupado {
  display: flex;
  position: relative;
  flex-direction: column;
  justify-content: center;
  text-align: center;
  width: 60%;
  height: 55%;
  padding: 25px;
  margin: 20px;
  background-color: #8d99ae;
  border-radius: 15px;
}

.parqueo h2 {
  color: #1b4965;
  font-family: "Fredoka One", cursive;
  font-size: 40px;
}

.parqueo_ocupado h2 {
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

@media only screen and (max-width: 423px) {
  .body h1 {
    font-size: 35px;
  }
  .parqueo {
    width: 65%;
    height: 45%;
    padding: 5px;
    margin: 10px;
  }
  .parqueo h2 {
    font-size: 30px;
  }
  .button {
    padding: 0.5em 0.5em;
    margin-bottom: 1em;
    font-size: 8px;
  }
}
</style>
