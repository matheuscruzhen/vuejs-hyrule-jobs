<template>
  <div class="job-list">
    <p class="order">Ordered by {{ order }}</p>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>
        <div class="salary">
          <img src="../assets/rupee.svg" alt="rupee" />
          <p>
            {{ job.salary }}
            rupees
          </p>
        </div>
        <div class="description">
          <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Sapiente
            magni eum animi laborum consectetur. Deleniti, officia veniam
            aperiam incidunt dolores harum minima, fugit dolorem amet mollitia
            et nihil consectetur veritatis!
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';
import type { PropType } from 'vue';

import type Job from '@/types/Job';
import type OrderTerm from '@/types/OrderTerm';

export default defineComponent({
  props: {
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return { orderedJobs };
  },
});
</script>

<style scoped>
.job-list {
  max-width: 960px;
  margin: 40px auto;
}

.job-list ul {
  padding: 0;
}

.job-list li {
  list-style-type: none;
  background-color: white;
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

.order {
  text-transform: capitalize;
  font-weight: bold;
}

.list-move {
  transition: all 1s;
}
</style>
