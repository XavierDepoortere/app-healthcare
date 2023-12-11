<template>
  <div class="LayoutRight" :style="{ width: expandedWidth }">
    <ProfilPatient />
  </div>
</template>

<script>
import ProfilPatient from "../components/ProfilPatient.vue";
export default {
  name: "LayoutRight",
  components: {
    ProfilPatient,
  },
  props: {
    expandedWidth: String,
  },
};
</script>

<style>
.LayoutRight {
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  background-color: #fafafa;
  border-radius: 1.5em;
  transition: width 0.5s ease-in-out;
}
</style>
