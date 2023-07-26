<template>
  <div class="app">
    <header>
      <div class="title">
          <img src="./assets/heart.svg" alt="site logo "/>
          <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="handleSort('title')">按标题排列</button>
        <button @click="handleSort('location')">按地点排列</button>
        <button @click="handleSort('salary')">按薪资排列</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobList from './components/JobList.vue'
import Job from './types/Job';
import OrderTerm from './types/OrderTerm';


export default defineComponent({
  name: 'App',
  components: {
    JobList
  },
  setup() {
    const jobs = ref<Job[]>([
      { title: "Bring Peace to Hyrule Field!", location: 'Hyrule Field, Central Hyrule', salary: 100, id: '1' },
      { title:"Mattison's Independence", location:'Tarrey Town, Akkala', salary: 200, id:'2'},
      { title:"The Horse Guard's Request", location:'Outskirt Stable, Central Hyrule', salary: 100, id:'3'},
      
    ])

    const order = ref<OrderTerm>('title');

    const handleSort = (term: OrderTerm) => {
      console.log(term);
      order.value = term;
    }

    return {jobs, handleSort, order}
  }, 
});
</script>

<style>
  header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
  header .title{
    display: flex;
    justify-content: center;
  }
  header img {
    width: 60px;
    margin-right: 20px;
  }
  header h1 {
    font-size: 3em;
  }
</style>
