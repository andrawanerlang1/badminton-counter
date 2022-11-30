<template >
  <b-container fluid class="container" style="color: white">
    <div>
      Andrawan's Badminton Counter</div>
    <b-container style="padding-top:25px;">
      <b-row style="background-color: rgb(8, 52, 8);">
        <b-col class="main-counter" :class="(counterA > 19 ? 'font-smaller' : '')" @click="increase('A')">{{ counterA
        }}</b-col>
        <b-col class="main-counter" :class="(counterB > 19 ? 'font-smaller' : '')" @click="increase('B')"> {{ counterB
        }}
        </b-col>
      </b-row>
      <b-row style=" background-color: rgb(8, 52, 8); padding-top: 10px;">
        <b-col class="reducer" @click="reduce('A')">-1</b-col>
        <b-col class="reducer" @click="reduce('B')">-1</b-col>
      </b-row>
      <b-row style="margin-top: 70px">
        <b-col class="serve-counter" @click="serve('A')">{{ serveA }}</b-col>
        <b-col class="serve-counter" @click="serve('B')"> {{ serveB }} </b-col>
      </b-row>
      <div>serve</div>
      <b-row style="margin-top: 70px">
        <b-col class="reset" @click="reset()">
          <b-icon icon="arrow-counterclockwise" font-scale="2"></b-icon>
        </b-col>
        <b-col class="reset" @click="change()">
          <b-icon icon="arrow-left-right" font-scale="2"></b-icon>
        </b-col>
      </b-row>
    </b-container>



  </b-container>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      counterA: 0,
      counterB: 0,
      serveA: "1st",
      serveB: ""
    };
  },
  methods: {
    increase(type) {
      if (type === 'A') {
        return this.counterA += 1
      } else {
        return this.counterB += 1

      }
    },
    reduce(type) {
      if (type === 'A') {
        if (this.counterA > 0) { return this.counterA -= 1 }
      } else {
        if (this.counterB > 0) { return this.counterB -= 1 }

      }
    },
    serve(type) {
      if (type === 'A') {
        if (this.serveA) {
          if (this.serveA === '1st') {
            this.serveA = '2nd'
          } else {
            this.serveA = '1st'
          }
        } else {
          this.serveA = '1st'
          this.serveB = ''
        }
      } else {
        if (this.serveB) {
          if (this.serveB === '1st') {
            this.serveB = '2nd'
          } else {
            this.serveB = '1st'
          }
        } else {
          this.serveB = '1st'
          this.serveA = ''
        }

      }
    },
    reset() {
      this.showMsgBoxOne()
      // this.counterA = 0
      // this.counterB = 0
      // this.serveA = "1st"
      // this.serveB = ""
    },
    change() {
      let temp = this.counterA
      this.counterA = this.counterB
      this.counterB = temp

      let temp2 = this.serveA
      this.serveA = this.serveB
      this.serveB = temp2
    },
    showMsgBoxOne() {
      this.$bvModal.msgBoxConfirm('Are you sure want to reset the score??', {
        okVariant: 'danger',
        cancelVariant: 'success',
        centered: true
      })
        .then(value => {
          if (value) {
            this.counterA = 0
            this.counterB = 0
            this.serveA = "1st"
            this.serveB = ""
          }
        })
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Wallpoet&display=swap');

.main-counter,
.reducer,
.serve-counter {
  font-family: 'Wallpoet', cursive;
}

.container {
  background-color: rgb(10, 73, 10);
  min-height: 100vh;
}

.main-counter {
  background-color: black;
  color: white;
  margin: 5px;
  height: 200px;
  font-size: 110px;
  font-weight: bolder;
  border-radius: 5%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.font-smaller {
  font-size: 80px;
}

@media (max-width: 370px) {
  .font-smaller {
    font-size: 60px;
  }
}

@media (max-width: 400px) {
  .font-smaller {
    font-size: 70px;
  }
}

.reducer {
  background-color: black;
  color: white;
  margin: 5px;
  padding-top: 7px;
  height: 40px;
  font-weight: bolder;
  text-align: center;
  border-radius: 5%;

}

.serve-counter {
  background-color: black;
  color: white;
  margin: 5px;
  padding-top: 8px;
  height: 100px;
  font-size: 50px;
  font-weight: bolder;
  text-align: center;
  border-radius: 5%;
}

.reset {
  background-color: black;
  color: white;
  margin: 5px;
  height: 70px;
  font-size: 20px;
  font-weight: bolder;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5%;

}
</style>
