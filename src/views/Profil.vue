<template>
  <div>
    <HeaderLogged />
    <ProfilComponent />
  </div>
</template>



<script>
// @ is an alias to /src
import HeaderLogged from "@/components/HeaderLogged.vue";
import ProfilComponent from "@/components/Profil.vue";

export default {
  name: "Profil",
  components: {
    HeaderLogged,
    ProfilComponent,
  },
};
</script>