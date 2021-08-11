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
      nav: [
        {
          link: '',
          txt: 'Про нас'
        },
        {
          link: '',
          txt: 'Оплата і доставка'
        },
        {
          link: '',
          txt: 'Бренди'
        },
        {
          link: '',
          txt: 'Контакти'
        }
      ],
      contacts: [],
      workingHours: []
    }
  },

  methods: {
    async fetchContacts() {
      try {
        const  contact = await axios.get('http://api.server347.com/13');
        const  workingHours = await axios.get('http://api.server347.com/14');
        this.contacts = contact.data;
        this.workingHours = workingHours.data;
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
