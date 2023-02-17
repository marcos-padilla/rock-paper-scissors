


<template>
  <div class="page">
    <PointsComponent :playerPoints="playerPoints" :cpuPoints="cpuPoints" />
    <span v-if="result" :style="{ color: result.color }">
      {{ result.text }}
    </span>
    <div class="buttons">
      <div class="button" @click="play('rock')">
        <img src="./assets/rock.png" />
      </div>
      <div class="button" @click="play('paper')">
        <img src="./assets/paper.png" />
      </div>
      <div class="button" @click="play('scissors')">
        <img src="./assets/scissors.png" />
      </div>
    </div>
    <button class="reset-button" @click="reset()">Reset</button>
  </div>
</template>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
}

.buttons {
  display: flex;
  margin-top: 10px;
  gap: 10px;
}

.button {
  border: 2px solid rgb(3, 197, 3);
  border-radius: 50%;
  padding: 5px;
  transition: .5s ease;
  cursor: pointer;
}

.button:hover {
  border: 4px solid rgb(3, 197, 3);
  box-shadow: 2px 2px 10px rgb(3, 197, 3);
}

.button>img {
  width: 50px;
}

.reset-button {
  margin-top: 10px;
}
</style>

<script>
import PointsComponent from './components/PointsComponent.vue';
const results = {
  player: { text: 'Player win', color: 'blue' },
  cpu: { text: 'CPU win', color: 'red' },
  tie: { text: 'Tie', color: 'rgb(3, 197, 3)' },
}
export default {
  components: {
    PointsComponent
  },
  data() {
    return {
      result: null,
      playerPoints: 0,
      cpuPoints: 0,
      timeout: null
    }
  },
  methods: {
    play(playerOption) {

      if (this.timeout) {
        clearTimeout(this.timeout)
        this.timeout = null
      }

      const options = ["rock", "paper", "scissors"];
      const machineOption = options[Math.floor(Math.random() * options.length)];
      if (playerOption === machineOption) {
        this.result = results.tie;
      } else if (
        (playerOption === "rock" && machineOption === "scissors") ||
        (playerOption === "paper" && machineOption === "rock") ||
        (playerOption === "scissors" && machineOption === "paper")
      ) {
        this.result = results.player;
        this.playerPoints++
      } else {
        this.result = results.cpu;
        this.cpuPoints++
      }
      this.timeout = setTimeout(() => {
        this.result = null
      }, 4000)
    },
    reset() {
      this.playerPoints = 0
      this.cpuPoints = 0
      this.timeout = null
      this.result = null
    }
  },
  created() {

    try {
      this.cpuPoints = JSON.parse(localStorage.getItem('cpuPoints')) || 0
      this.playerPoints = JSON.parse(localStorage.getItem('playerPoints')) || 0
    } catch (e) {
      this.cpuPoints = 0
      this.playerPoints = 0
    }
  },
  updated() {
    localStorage.setItem('cpuPoints', JSON.stringify(this.cpuPoints))
    localStorage.setItem('playerPoints', JSON.stringify(this.playerPoints))
  }
}
</script>