<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <h1 class="text-center">鈴聲設定</h1>
      </v-col>
      <v-col cols="12">
        <v-table style="background: #57c51b">
          <thead>
            <tr>
              <th>名稱</th>
              <th>試聽</th>
              <th>選擇</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="alarm in alarms" :key="alarm.id">
              <td>{{ alarm.name }}</td>
              <td>
                <audio :src="alarm.file" controls class="custom-audio"></audio>
              </td>
              <td>
                <v-radio-group v-model="selectedAlarm">
                  <v-radio :value="alarm.id"></v-radio>
                </v-radio-group>
              </td>
            </tr>
          </tbody>
        </v-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { definePage } from "vue-router/auto";
import { useSettingsStore } from "@/stores/settings";
import { storeToRefs } from "pinia";

definePage({
  meta: {
    title: "番茄鐘 | 設定",
  },
});

const settings = useSettingsStore();
const { alarms, selectedAlarm } = storeToRefs(settings);
</script>

<style scoped lang="scss">
:deep(.v-input__details) {
  display: none;
}
.custom-audio {
  color: #87d65c; /* 例如：黑色控制項 */

  &::-webkit-media-controls-panel {
    background-color: #87d65c; /* 改變控制面板背景顏色 */
  }
}
</style>
