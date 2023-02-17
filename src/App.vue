


<template>
  <div class="page">
    <PointsComponent />
    <span v-if="result" :style="{ color: result.color }">
      {{ result.text }}
    </span>
    <div class="buttons">
      <div class="button">
        <img src="./assets/rock.png" />
      </div>
      <div class="button">
        <img src="./assets/paper.png" />
      </div>
      <div class="button">
        <img src="./assets/scissors.png" />
      </div>
    </div>
    <button class="reset-button">Reset</button>
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
  tie: { text: 'tie', color: 'rgb(3, 197, 3)' },
}
export default {
  components: {
    PointsComponent
  },
  data() {
    return {

      result: results.cpu
    }
  }
}
</script>