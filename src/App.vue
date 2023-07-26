<template>
  <div class="app">
    <header>
      <div class="title">
          <img src="./assets/heart.svg" alt="site logo "/>
          <h1>Hyrule Jobs</h1>
      </div>
      <div class="order">
        <MyButton class="btn" text="按标题" :size="12"  @click="handleSort('title')" />

        <!-- <button @click="handleSort('title')">按标题</button> -->
        <MyButton class="btn" text="按地点" :size="12" @click="handleSort('location')" />
        <MyButton class="btn" text="按报酬" :size="12" @click="handleSort('salary')" />
      </div>

    </header>

    <div class="add">
      <MyButton text="创建新任务" color="#17bf66" bgcolor="#fff" :size="undefined" @click="openModal" />
      <!-- <button class="btn" @click="openModal">创建新任务</button> -->
    </div>
    <JobList :jobs="jobs" :order="order"/>
    <transition name="fade">
      <NewQuest v-if="showModal" @close-modal="openModal"  @add-quest="addQuest"/>
    </transition>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobList from './components/JobList.vue'
import Job from './types/Job';
import OrderTerm from './types/OrderTerm';
import NewQuest from './components/NewQuest.vue'
import MyButton from './components/MyButton.vue'


export default defineComponent({
  name: 'App',
  components: {
    JobList, NewQuest, MyButton
  },
  setup() {
    const jobs = ref<Job[]>([
      { title: "Bring Peace to Hyrule Field!", location: "Hyrule Field, Central Hyrule", salary: 100, id: "1",content:"1. Talk to Hoz and start the quest. Once you approach the location, you will find the captain, Hoz, and his crew on the field. Talk to him. ...  2. Find the monster stronghold. Go with the crew, and you will find the monster stronghold behind the trees. 3. Defeat monsters ... 4. Talk to Hoz again once you have defeated all enemies. ..." },
      { title:"Mattison's Independence", location:"Tarrey Town, Akkala", salary: 200, id:'2',content:""},
      { title: "The Horse Guard's Request", location: "Outskirt Stable, Central Hyrule", salary: 100, id: "3", content:""},
    ])

    const order = ref<OrderTerm>('title');

    const handleSort = (term: OrderTerm) => {
      order.value = term;
    }

    // modal
    const showModal = ref(false)
    const openModal = () => {
      showModal.value =!showModal.value;
    }

    // add quest
    const addQuest = (e: Job) => {
      jobs.value.push(e)
    }

    return {jobs, handleSort, order, showModal, openModal, addQuest}
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
  /* button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  } */
  .order .btn{
    display: inline-block;
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
  .add{
    display: flex;
    flex-direction: row;
    justify-content: flex-end;
    max-width: 960px;
    margin: 40px auto;
  }

  .add .btn{
    border-color: #17bf66;
    color: #17bf66;
    height: 46px;
    padding: 2px 8px;
    border-radius: 8px;
   }
   .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
</style>
