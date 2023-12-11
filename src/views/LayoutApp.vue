<template>
  <div class="Layout">
    <SidebarApp />
    <div id="content" :class="{ hidden: isLayoutExpanded }">
      <CardProfil
        :patient="selectedPatient"
        @view-profile="handleViewProfile"
      />
      <h3>Liste Patients</h3>
      <CardListPatient
        :data_patient="data_patient"
        @patient-selected="updateProfileCard"
      />
    </div>
    <LayoutRight :expandedWidth="expandedWidth" />
  </div>
</template>

<script>
import bdd_patient from "../bdd_patient";
import { onMounted, ref, computed } from "vue";
import CardListPatient from "../components/CardListPatient.vue";
import SidebarApp from "../components/SidebarApp.vue";
import LayoutRight from "./LayoutRight.vue";
import CardProfil from "../components/CardProfil.vue";
export default {
  name: "LayoutApp",
  components: {
    CardListPatient,
    LayoutRight,
    CardProfil,
    SidebarApp,
  },

  data() {
    class Patient {
      constructor(id, image, prenom, nom, date_naissance, poids, taille, sexe) {
        this.id = id;
        this.image = image;
        this.prenom = prenom;
        this.nom = nom;
        this.date_naissance = date_naissance;
        this.poids = poids;
        this.taille = taille;
        this.sexe = sexe;
      }
    }
    let data_patient = ref([]);
    const selectedPatient = ref(null);
    const expandedWidth = ref("74%");
    const makeListPatient = () => {
      bdd_patient.forEach((patient) => {
        const new_patient = new Patient(
          patient.id,
          patient.image,
          patient.prenom,
          patient.nom,
          patient.date_naissance,
          patient.poids,
          patient.taille,
          patient.sexe
        );
        data_patient.value.push(new_patient);
      });
    };
    const updateProfileCard = (patient) => {
      selectedPatient.value = patient;
    };

    const handleViewProfile = () => {
      expandedWidth.value = "90%";
    };

    const isLayoutExpanded = computed(() => {
      return expandedWidth.value > "74%";
    });
    onMounted(makeListPatient);
    onMounted(() => {
      if (data_patient.value.length > 0) {
        selectedPatient.value = data_patient.value[0];
      }
    });

    return {
      data_patient,
      selectedPatient,
      expandedWidth,
      updateProfileCard,
      handleViewProfile,
      isLayoutExpanded,
    };
  },
};
</script>

<style>
.Layout {
  display: flex;
  justify-content: space-between;
  float: left;
  position: fixed;
  z-index: 1;
  top: 1%;
  left: 2.5%;
  bottom: 2.5%;

  border-radius: 1.5em;
  background-color: #f0f0f0;
  width: 95vw;
  height: 98vh;
}
.hidden {
  display: none;
}
</style>
