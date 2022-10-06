<template>
  <div>
    <v-row>
      <v-col sm="12" md="12" lg="12">
        <h2>DashBoard</h2>
      </v-col>
    </v-row>
    <div v-if="groupDashboardData.group">
      <h3>{{ groupDashboardData.group.name }}</h3>
      <v-row>
        <v-col sm="12" md="12" lg="12">
          <v-simple-table>
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left">Name</th>
                  <th class="text-left">Status</th>
                  <th class="text-left">Waiting</th>
                  <th class="text-left">Paused</th>
                  <th class="text-left">Active</th>
                  <th class="text-left">Delayed</th>
                  <th class="text-left">Failed</th>
                </tr>
              </thead>
              <tbody v-if="groupDashboardData.queues">
                <tr v-for="item in groupDashboardData.queues" :key="item.id">
                  <td>{{ item.name }}</td>
                  <td>{{ item.status }}</td>
                  <td>{{ item.jobCounts.waiting }}</td>
                  <td>{{ item.jobCounts.paused }}</td>
                  <td>{{ item.jobCounts.active }}</td>
                  <td>{{ item.jobCounts.delayed }}</td>
                  <td>{{ item.jobCounts.failed }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { DashGroup } from "~/types/group";
export default Vue.extend({
  middleware: 'auth',
  name: "IndexPage",
  data() {
    return {
      groupDashboardData: {} as DashGroup,
    };
  },
  async created() {
    this.groupDashboardData = await this.$api.dashboard.groupDashById(this.$route.params.id)
    console.log(this.groupDashboardData.queues.length)
    console.log(this.groupDashboardData.group.name)
  },
});
</script>
