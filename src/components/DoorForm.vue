<script>
let idCounter = 0;

function uniqueId(prefix) {
  var id = ++idCounter;
  return toString(prefix) + id;
}

export default {
  emits: ['response'],
  name: 'DoorForm',
  props: {
    msg: String,
    tmp: Number
  },
  data() {
    console.log(this.sum)
    return {
      points: [],
      sum: 0
    };
  },
  methods : {
    addDoor(){
      this.points.forEach((point) => {
        const sum = point.widthD * point.heightD
        point.sum = sum
        this.sum += sum
      })

      this.points.push({
        id: uniqueId(),
        widthD: '',
        heightD: '',
        sum: ''
      });
    },
    deleteDoor(counter){
      this.points.splice(counter,1);
    },
  },
};
</script>

<template>
  <div id="door">
    <h1>Проём</h1>
    <p class="mt-10 text-5xl font-bold"> 
      <img src=".././assets/proem.jpeg">
    </p>
    <form>
      <button @click="addDoor">Добавить проем</button>
      <br>
      <div
      v-for="(wh, counter) in points"
      v-bind:key="counter">
        <button @click="deleteDoor(counter)">x</button>
        <label for="duration">{{counter+1}}. Ширина проёма:</label>
        <input v-model="wh.widthD" required>
        <label for="duration"> Высота проема:</label>
        <input v-model="wh.heightD" required>
      </div>
    </form>
</div>

</template>