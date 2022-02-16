<template>
  <div class="app">
    <h1>Rejse Udligning</h1>
    <div class="start" v-show="start">
      <input type="text" v-model="pname" />
      <button @click="addPerson(pname)">Tilføj person</button>
      <br />
      <br />
      <button @click="onTrip()">Start rejse</button>
    </div>

    <div class="group">
      <h2>Rejsedeltagere</h2>
      <div v-for="p in persons" :key="p.id">
        <p>{{ p.name }}</p>
        <div class="during" v-show="during">
          <input type="text" @input="expense = $event.target.value" />
          <button @click="addExpense(expense)">Tilføj udgift</button>
          <p>Saldo: {{ p.wallet }} kr. </p>
        </div>
      </div>
    </div>

    <div class="during" v-show="during">
      <p>Samlede udgifter: {{ totalexpenses }} kr</p>
    </div>

    <div class="end" v-show="end">
      <p>Slut</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Person from "./types/Person";
import Expense from "./types/Expense";

export default defineComponent({
  name: "App",
  components: {},
  setup() {
    const persons = ref<Person[]>([])
    const expenses = ref<Expense[]>([])
    return { persons, expenses }
  },
  data() {
    return {
      pid: 1,
      pname: "",
      start: true,
      during: false,
      end: false,
      totalexpenses: 0,
      expense: 0
    };
  },
  methods: {
    onTrip() {
      if (this.persons.length != 0) {
        this.start = !this.start;
        this.during = !this.during;
      }
    },
    addPerson(name: string) {
      if (name != null && name.length != 0) {
        console.log(name)
        this.persons.push({ id: this.pid, name: name, wallet: 0 });
        console.log(this.persons);
        this.pid++;
        this.pname = "";
      }
    },
    addExpense(amount: number) {
      console.log("Amount " + amount)
      let selfpay = (1/this.persons.length*amount)
      console.log("Self pay " + selfpay)
      let exclselfpay = amount-selfpay
      console.log("Rest pay " + exclselfpay)

      this.totalexpenses = this.totalexpenses + Number(amount)
    }
  },
});
</script>

<style>
</style>
