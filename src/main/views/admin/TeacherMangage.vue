<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>#</th>
          <th>姓名</th>
          <th>职称</th>
          <th>手机号</th>
          <th>简介</th>
          <th>
            <addTeacher v-bind:allTeachers="allTeachers" />
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(t, index) in allTeachers" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ t.name }}</td>
          <td>{{ t.title }}</td>
          <td>{{ t.phoneNumber }}</td>
          <td style="width:30%">{{ t.intro }}</td>
          <td>
            <div class="operationButton">
              <div v-if="role == '2356afcd332d'">
                <button @click="manageAdmin(t)" v-if="t.authority == 1">
                  设为管理员
                </button>
                <button @click="manageAdmin(t)" v-if="t.authority == 2">
                  取消管理员
                </button>
              </div>
              <fixTeacherInfo v-bind:teacher="t" />
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import bus from "@/util/Bus";
import { listTeachers } from "@/main/api/Main";
import { setAdmin } from "@/main/api/Main";

export default {
  components: {
    addTeacher: () => import("./AddTeacher.vue"),
    fixTeacherInfo: () => import("./FixTeacherInfo.vue")
    // detailButton: () => import("./DetailButton.vue")
  },
  data() {
    return {
      allTeachers: null,
      role: null
    };
  },
  created() {
    listTeachers();
    bus.$on(bus.allTeachers, data => {
      console.log(data);
      this.allTeachers = data;
    });
    this.role = sessionStorage.getItem("role");
    // console.log(this.role);
  },
  beforeDestroy() {
    bus.$off(bus.allteachers);
  },
  methods: {
    manageAdmin(t) {
      setAdmin(t);
      t.authority = t.authority == 1 ? 2 : 1;
    }
  }
};
</script>

<style scoped>
.operationButton {
  display: flex;
  justify-content: center;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th,
td {
  text-align: center;
  /* padding: 8px; */
}

tbody tr:nth-child(odd) {
  background-color: #0000000e;
}
button {
  margin: 5px;
}
</style>
