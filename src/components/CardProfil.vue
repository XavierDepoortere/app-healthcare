<template>
  <div v-if="patient" class="CardProfil">
    <img :src="patient.image" alt="" />
    <div class="info">
      <div class="username">{{ patient.prenom }} {{ patient.nom }}</div>
      <div class="link-profil" @click="viewProfile">Voir profil</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    patient: Object,
  },
  methods: {
    viewProfile() {
      this.$emit("view-profile");
      console.log("test");
    },
  },
};
</script>

<style lang="scss">
.CardProfil {
  display: flex;
  position: relative;
  z-index: 1;
  background-color: #fbfbfb;
  width: 15vw;
  height: 18vh;
  border-radius: 2em;
  margin-top: 5em;
  img {
    position: absolute;
    left: 50%;
    top: -35%;
    transform: translateX(-50%);

    width: 6em;
    border-radius: 50%;
  }
  .info {
    display: flex;
    flex-direction: column;
    width: 100%;
    align-items: center;

    .username {
      font-size: 1.5em;
      font-weight: bold;
      margin: 2.5em 0 0.5em 0;
    }
    .link-profil {
      color: #c8c8c8;
      cursor: pointer;
    }
  }
}
</style>
