<template>
  <div class="CardListPatient">
    <div class="list">
      <div
        class="rowList"
        v-for="(data, i) in displayedPatients"
        :key="i"
        @click="selectPatient(data)"
      >
        <img :src="data.image" alt="" />
        <div class="info-patient">
          <div class="name">{{ data.prenom }} {{ data.nom }}</div>
          <div class="id">ID: {{ data.id }}</div>
        </div>
      </div>
    </div>
    <div class="search">
      <span class="material-icons"> search </span
      ><input v-model="search_patient" type="text" placeholder="Recherche..." />
    </div>
  </div>
</template>

<script>
import { ref, watch, computed } from "vue";
import data_patient from "../bdd_patient";
export default {
  name: "CardListPatient",
  props: {
    data_patient: Array,
  },
  methods: {
    selectPatient(patient) {
      this.$emit("patient-selected", patient);
    },
  },
  data() {
    let search_patient = ref("");
    let filteredPatients = ref([]);
    watch(search_patient, (newValue) => {
      if (newValue) {
        const regex = RegExp(newValue, "i");
        filteredPatients.value = data_patient.filter(
          (patient) =>
            regex.test(patient.nom) ||
            regex.test(patient.id) ||
            regex.test(patient.prenom)
        );
      } else {
        filteredPatients.value = data_patient;
      }
    });

    const displayedPatients = computed(() =>
      filteredPatients.value.length > 0 ? filteredPatients.value : data_patient
    );

    return {
      search_patient,
      filteredPatients,
      displayedPatients,
    };
  },
};
</script>

<style lang="scss">
.CardListPatient {
  display: flex;
  flex-direction: column;
  position: relative;
  background-color: #fbfbfb;
  width: 15vw;
  height: 53vh;
  border-radius: 2em;
  margin-top: 1em;
  padding-top: 1em;
  .list {
    height: 325px;
    overflow-y: scroll;
    overflow-x: hidden;
    margin-top: 3px;
    margin-bottom: 3px;
    &::-webkit-scrollbar {
      display: none;
    }
    -ms-overflow-style: none;

    scrollbar-width: none;
  }

  .rowList {
    display: flex;
    align-items: center;
    width: 100%;
    height: 4em;
    cursor: pointer;
    &:hover {
      background-color: #f0f0f0;
    }

    img {
      width: 3em;
      height: 3em;
      border-radius: 50%;
      margin-left: 1em;
    }
    .info-patient {
      display: flex;
      flex-direction: column;
      margin-left: 1em;
      .name {
        font-weight: bold;
      }
      .id {
        font-size: 0.8rem;
        color: #c8c8c8;
      }
    }
  }
  .search {
    display: flex;
    margin: 1em;
    color: #fbfbfb;
    background-color: #56c157;
    border: none;
    height: 2.2em;
    border-radius: 2em 2em 2em 2em;
    .material-icons {
      display: flex;
      align-items: center;
      justify-content: center;
      border: none;
      height: 2.2em;
      outline: none;
      width: 20%;
      height: 100%;
    }
    input {
      color: #fbfbfb;
      background-color: transparent;
      border: none;
      height: 2.2em;
      outline: none;
      width: 75%;
      height: 95%;
      &::placeholder {
        color: #fbfbfb;
      }
    }
  }
}
</style>
