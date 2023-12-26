<template>
  <div class="home flex-grow-1 d-flex flex-column align-items-center justify-content-center">
    <section>
      <img v-if="bossHealth > 0" class="oslo" src="https://em-content.zobj.net/source/twitter/348/orangutan_1f9a7.png" alt="Evil Oslo">
      <img v-else class="oslo dead" src="https://em-content.zobj.net/source/twitter/348/orangutan_1f9a7.png" alt="Evil Oslo">
      <h3 class="fw-bold">Evil Oslo</h3>
      <h1>{{ bossHealth }}</h1>
      <div class="progress">
        <div :class="`progress-bar bg-${healthColor}`" role="progressbar" :style="`width: ${bossHealth}%;`" >
          {{bossHealth}} {{ belowHalf }}
        </div>
      </div>
      <!-- <button class="btn btn-danger" @click="killEvilOslo()" >🔪</button> -->
      <button v-for="attack in attacks" class="btn btn-danger" @click="killEvilOslo(attack.damage)" >{{ attack.emoji }}{{attack.damage}}</button>

    </section>
  </div>
</template>

<script>
import {computed, ref} from 'vue'
export default {
  setup() {
// regular js + vue magic
// const bossHealth = 100 just regular js ☹️
const bossHealth = ref(100) // vue magic ✨
const maxHealth = 100

const belowHalf = computed(()=> bossHealth.value < 51)

function killEvilOslo(damage){
  bossHealth.value -= damage
}

const attacks = [{emoji: '🔪', damage: 5}, {emoji: '⚔️',damage: 10}, {emoji:'🔥', damage: 50}]


return {
  // Anything our template wants to draw / call
  attacks,
  bossHealth,
  belowHalf,
   healthColor : computed(()=> bossHealth.value < 51 ? 'warning': 'success'),
      killEvilOslo
    }
  }
}
</script>

<style scoped lang="scss">
.home {
  display: grid;
  height: 80vh;
  place-content: center;
  text-align: center;
  user-select: none;

  .home-card {
    width: clamp(500px, 50vw, 100%);

    >img {
      height: 200px;
      max-width: 200px;
      width: 100%;
      object-fit: contain;
      object-position: center;
    }
  }
}

.oslo{
  filter: hue-rotate(45deg);
}

.dead{
  transform: rotate(45deg);
}

</style>
