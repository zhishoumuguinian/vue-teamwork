<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>课程名称</th>
          <th>开始时间</th>
          <th>结束时间</th>
          <th>地点</th>
          <th>完成情况</th>
          <th>
            <addInvigilation v-bind:invigilations="invigilations" />
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(a, index) in invigilations" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ a.exam.name }}</td>
          <!-- 开始时间 -->
          <td>{{ formatDate(a.exam.startTime) }}</td>
          <!-- 结束时间 -->
          <td>{{ formatDate(a.exam.overTime) }}</td>
          <!-- 地点 -->
          <td>{{ a.exam.classroom }}</td>
          <!-- 完成情况 -->
          <td>{{ a.invigilation.state }}</td>
          <td>
            <detailButton v-bind:assigment="a" v-if="invigilations.length" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import bus from "@/util/Bus";
import { listAllAssigmentsByAdmin } from "@/main/api/Main";

export default {
  components: {
    detailButton: () => import("./DetailButton.vue"),
    addInvigilation: () => import("./AddInvigilation.vue")
  },
  data() {
    return {
      invigilations: []
    };
  },
  created() {
    // console.log("invigilations.vue");
    listAllAssigmentsByAdmin();
    bus.$on(bus.allAssigments, data => {
      this.invigilations = data;
      // console.log("invigilations.vue created");
    });
  },
  beforeDestroy() {
    // console.log("invigilations.vue beforeDestroy");
    bus.$off(bus.allAssigments);
  },
  computed: {
    formatDate() {
      return date => (date == null ? null : date.replace("T", " "));
    }
  }
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
th,
td {
  text-align: center;
  padding: 8px;
}

tbody tr:nth-child(odd) {
  background-color: #0000000e;
}
</style>
