<script setup lang="ts">
import { ref, watch } from "vue";
import { type AlertInfo, newAlert } from "../utils";

// 定义 Map，存储Alert信息集合，使用Map便于删除
const alertMap = ref<Map<string, AlertInfo>>(new Map());

// 监听新Alert创建
watch(newAlert.value, () => {
  alertMap.value.set(newAlert.value.id, { ...newAlert.value });
  // console.log(alertMap.value);
  deleteAlert(newAlert.value.id);
});

const deleteAlert = (id: string) => {
  // console.log(id);
  setTimeout(() => {
    alertMap.value.delete(id);
  }, 3000);
};
</script>

<template>
  <div class="alert-container">
    <v-alert
      class="v-alert"
      v-for="(alert, index) in Array.from(alertMap.values())"
      :key="index"
      :type="alert.type"
      closable
      close-label="Close Alert"
      :text="alert.message"
    >
    </v-alert>
  </div>
</template>

<style scoped>
.alert-container {
  position: absolute;
  bottom: 5%;
  left: 5%;
}

@media screen and (max-width: 1280px) {
  .alert-container {
    left: 5%;
  }
}

.v-alert {
  margin-top: 0.2rem !important;
  z-index: 9999;
}
</style>
