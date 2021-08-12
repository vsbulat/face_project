<template>
    <div class="layout">
      <app-header
          :nav="nav"
          :contacts="contacts"
          :workingHours="workingHours"
      />
<!--      <router-view></router-view>-->
    </div>

  <app-footer
      :nav="nav"
      :contacts="contacts"
      :workingHours="workingHours"
      :footerNav="footerNav"
  />
</template>


<script>
import "@/style/style.scss"
import AppHeader from "@/components/shared/header/app-header";
import AppFooter from "@/components/shared/footer/app-footer";
import axios from "axios"
export default {
  components: {AppFooter, AppHeader},
  data() {
    return {
      nav: [],
      contacts: [],
      workingHours: [],
      footerNav: []
    }
  },

  methods: {
    async fetchContacts() {
      try {
        const  contact = await axios.get('http://api.server347.com/13');
        const  workingHours = await axios.get('http://api.server347.com/14');
        const  nav = await axios.get('http://api.server347.com/15');
        const  footerNav = await axios.get('http://api.server347.com/16');
        this.contacts = contact.data;
        this.workingHours = workingHours.data;
        this.nav = nav.data;
        this.footerNav = footerNav.data;
      } catch (e) {
        alert("Alert!!!")
      }

    }
  },

  mounted() {
    this.fetchContacts();
  }
};

</script>
<style></style>
