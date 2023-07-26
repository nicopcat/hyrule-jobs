<template>
  <div class="job-list">
     <p>按 {{ order }}</p>
    <ul >
      <transition-group name="list" tag="ul">
        <li v-for="job in filteredList" :key="job.id">
          <h3>{{ job.title }} @{{ job.location }}</h3>
          <div class="salary">
            <img src="@/assets/rupee.svg" />
            <p>{{ job.salary }} 卢比</p>
          </div>
          <div class="description">
            <p>
              {{ job.content }}
            </p>
          </div>
        </li>
      </transition-group>
    </ul>

  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from 'vue';
import Job from '@/types/Job'
import OrderTerm from '@/types/OrderTerm';

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup(props) {
    
    const filteredList = computed(() => {
      // 扩展运算符 ... 对 props.jobs 数组进行浅拷贝
      return [...props.jobs].sort((a: Job, b: Job) => {
          if (a[props.order] < b[props.order]) {
            return -1;
          } else if (a[props.order] > b[props.order]) {
            return 1;
          } else {
            return 0;
          }
      })
    });

    return {filteredList}
  }
})

</script>

<style scoped>
  /* by Shuan  */
  .job-list {
    max-width: 960px;
    margin: 40px auto;
  }

  .job-list ul {
    padding: 0
  }
 .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
    transition: all 1s;
  }

/* by chatGPT  */

.job-list li {
  transition: transform 0.3s ease-in-out;
}

.job-list li:hover {
  transform: translate(5px, -5px);
}


</style>